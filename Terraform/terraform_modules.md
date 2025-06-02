**Terraform Modules**
- moduleas are also functions in which we pass inputs and we get infra
```
//not mandatory
variable "ami_id"{
default=""
}
//mandatory
variable "sg_id"{

}
```
```
variable "instance_type"{
    default= "t3.micro"
    validation{
        condition = contains(["t3.micro","t3.small","t3.medium"],instance_type)
        error_message="Valid values are : t3.micro,t3.small,t3.medium"
    }
}
```

**Module**
- which ever value we mention in while using the module will be overridden inside actula module
- in modules outputs are equally important,hey should also be mentioned
- after creating the resources it will have the ips,ids etc,those can be printed by output command
- again in module user wants to use to print then again he has to mention the outputblock in the usage
```
output "public_ip"{
    value=module.<module_name>.<output_block_name>
}
```
```
module 'ec2'{
    source=../<dir>
}
```
