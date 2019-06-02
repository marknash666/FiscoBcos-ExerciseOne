# Lab-One Illustration of Build_Chain.sh 

## Part One 
### 1. main function
First of all, we can go to line 904.

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
There is no doubt that this is the start of the sh file, we can see the exception handling when we forget to add the -l or -f parameter in this part of code. Let's start from here and trace the building of FISCO BCOS's Consortium Blockchain.

`dir_must_not_exists ${output_dir}
mkdir -p "${output_dir}"`

The code in line 920 and 921 call the *dir\_must\_not\_exists* function to checked that there is no such a file directory as nodes (the default value of *output_dir* is "nodes") and creat the directory, else it'll throw an exception.

Then, the code from line 929 to 959 checks whether we are using docker mode (if we use macos, we have to either use docker mode or use -e option to specific fisco-bcos binary path) , after that it would download the the corresponding version of binary files or check the existing files to ensure the match of version.

Then, the code from line 960 to 965 uses *generate\_cert_conf* function to generate a cert config file or copy the designated file to the current directory.

Then, the code from line 976 to 991 would check whether we have an existing CA file. If not, the code would call the *gen_chain_cert* and *gen_agency_cert* function to generate ca.key.

Then, the code from line 993 to 1004 would check whether we choosed to build a blockchain of GuoMi version. If yes, the code would call the *check_and_install_tassl* to first create a TASSL environment, and use *generate_cert_conf_gm* function to generate gmcert.cnf configuration file. The following process is similar to the described process aboved, and the functions are replced by the GuoMi version.

The code from line 1008 to 1117 would check whether we choosed to build a blockchain of GuoMi version. If yes, the code would call the *check_and_install_tassl* to first create a TASSL environment, and use *generate_cert_conf_gm* function to generate gmcert.cnf configuration file. The following process is similar to the described process aboved, and the functions are replced by the GuoMi version.











