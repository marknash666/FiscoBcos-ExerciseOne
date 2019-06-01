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

