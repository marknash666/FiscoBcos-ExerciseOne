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

The code in line 920 and 921 call the dir\_must\_not\_exists function to checked that there is no such a file directory as nodes (the default value of *output_dir* is "nodes") and creat the directory, else it'll throw an exception.

Then, the code from line 929 to 959 checks whether we are using docker mode (if we use macos, we have to either use docker mode or use -e option to specific fisco-bcos binary path) , after that it would download the the corresponding version of binary files or check the existing files to ensure the match of version.

Then, the code from line 960 to 965 uses generate_cert_conf function to generate a cert config file or copy the designated file to the current directory.








