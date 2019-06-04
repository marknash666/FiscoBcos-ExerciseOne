# Lab-One Illustration of Build_Chain.sh 


## Implementation body
The last four row of code shown below are the functions called during the actual implementation of the shell file.
```
check_env
parse_params $@
main
print_result
```

## Part One - check_env()
```
check_env() {
    [ ! -z "$(openssl version | grep 1.0.2)" ] || [ ! -z "$(openssl version | grep 1.1)" ] || [ ! -z "$(openssl version | grep reSSL)" ] || {
        echo "please install openssl!"
        #echo "download openssl from https://www.openssl.org."
        echo "use \"openssl version\" command to check."
        exit $EXIT_CODE
    }
    if [ ! -z "$(openssl version | grep reSSL)" ];then
        export PATH="/usr/local/opt/openssl/bin:$PATH"
    fi
    if [ "$(uname)" == "Darwin" ];then
        OS="macOS"
    elif [ "$(uname -s)" == " Linux " ];then
        OS="Linux"
    fi
}

```
This function ensures that the user's environment is capable of running the following code. It checks the existence of openssl (-z String would be true while the length of String is zero, so the first judgment means that the shell would stop running when there is no any version of openssl) and save the typre ofcurrent system into parameter OS.

## Part Two - parse_params()

This part of code processes the options we set when implementing the shell file. Detailed explanation can refer to [here][1]. For the previous Exercise on class, we used the -l option to specify the chain to be generated and the number of nodes under each IP.
[1]:https://fisco-bcos-documentation.readthedocs.io/zh_CN/latest/docs/manual/build_chain.html#id4

## Part Three - main()
### 1. Option Check
First of all, we go to line 904.

```
   main()
{
output_dir="$(pwd)/${output_dir}"
[ -z $use_ip_param ] && help 'ERROR: Please set -l or -f option.'
if [ "${use_ip_param}" == "true" ];then
    ip_array=(${ip_param//,/ })
elif [ "${use_ip_param}" == "false" ];then
    if ! parse_ip_config $ip_file ;then 
        echo "Parse $ip_file error!"
        exit 1
    fi
else 
    help 
fi
```
There is no doubt that this is the main implementation of the shell file. we can see the exception handling when we forget to add the -l or -f parameter in this part of code. Let's start from here and trace the building of FISCO BCOS's Consortium Blockchain.

```
dir_must_not_exists ${output_dir}
mkdir -p "${output_dir}"
```
The code in line 920 and 921 call the *dir\_must\_not\_exists* function to checked that there is no such a file directory as nodes (the default value of *output_dir* is "nodes") and create the directory, else it'll throw an exception.

### 2. Binary File Processsing
The code from line 929 to 959 checks whether we are using docker mode (if we use macos, we have to either use docker mode or use -e option to specific the path of fisco-bcos binary) . After that, it would download the the corresponding version of binary files or check the existing files to ensure the match of version.

### 3. Generate Certification Configuration 
In line 960 to 965, the bash uses *generate\_cert_conf* function to generate a certification config file or copy the designated file to the current directory.

### 4. CA key 
The code from line 976 to 991 would check whether we have an existing CA file. If not, the code would call the *gen_chain_cert* and *gen_agency_cert* function to generate ca.key.

### 5. GuoMi Chain(optional) CA key
The bash provides with a guomi_mode option that would enable the building of a blockchain of GuoMi version. If the option is set to true, the bash would call the *check_and_install_tassl* to first create a TASSL environment, and use *generate_cert_conf_gm* function to generate gmcert.cnf configuration file. The following process is similar to the described process in 4, while the functions are replced by the GuoMi version, for instance, *gen_chain_cert* is replaced by *gen_chain_cert_gm*.

### 6. Generating Key 
The code from line 1008 to 1025 would set up the paramters that is related to the node generating for each IP server designated, and there is a double loop in the loop for every IP. 

Line 1026 to 1107 is a Double Loop. The outer level of Loop is determined by the numbers of nodes, it would first check the existence of the directory and throws exception when the directory already exists. 

The inner Loop would do the following:

1. call *gen_node_cert* to generate cetification of nodes, create a configuration file directory(the default value of *conf_path* is conf), then removes the unwanted files and finally moves all the file in the current directory to the conf directory.
2. checks the length and the first two number of privateKey to ensure its legality, otherwise the whole node directory would be deleted.
3. do the similar privateKey checking when the GuoMi option is enabled. The differences are that conf_path is replaced by gm_conf_path and the privateKey of GuoMi should start with "00"

We now come back to the outer loop, this part of code do different operation to the configuration files in accordance with GuoMi or non-GuoMi, set the node_groups if we used -f option and set the nodeid_list if we used -l option.












