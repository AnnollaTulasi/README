**LOOPS**
1. count based loop  - iterate over list type of variables
2. for each loops - used to iterate maps
3. dynamic blocks

**Functions**
- we will not have custom functions
length,join,split,max,min,upper,lower,startswith,merge-if we have same parameter in 2nd variable,it will override the first one

**Data Sources And Output**
- existing information from provider(aws,azure) can be queried using data sources
- output is to print the queried data,used in module development
```
data "aws_ami" "joindevops"{
most_recent=true
and some other filers has to be added
}

output "ami_id"{
    value=data.aws_ami.joindevops.id
}
```

**Locals**
- are used to run the expressions and save the results to variables
- readability increases because of locals
- if we add the variables in locals then they will not be overridden
- we cannot use the variables in variable 
eg:
```
variable "environment"{
    default= dev
}
varaiable "project"{
    default= "expense"
}
variable "name"{
    default = "${var.project}-${var.environment}"
}
```
```
locals{

}
```
**State Management**
- Terraform has one state file ,in that all the changes which we do from code are noted and it compares to actual infra in provider,if any one changes from provider side it will pick again from statefile and modify the changes
- we should not do changes in tfstate file
- statefile should be centralized and should be secure
- if statefile is not centralized then we will have duplicate resources or error(Security Group cannot be duplicated)
- locks will protect from parallel execution
* Create a bucket and using dynamodb will do the locking
```
terraform{
    backend "s3"{
        bucket= <bucket_name>
        key= 
        region= 
        dynamodb_table=
    }
}
```
=================================
**DYNAMIC BLOCKS**
- count based loops are used to create multiple resources
- dynamic blocks are used to create multiple blocks inside the resource
```
dynamic "ingress"{ # with blockname we can access the loop items
    for_each=var.ingress_ports
    content{
        from_port=ingress.value["from_port"]
        to_port=ingress.value["to_port"]
    }
}

variable "ingress_ports"{
    default=[
        {
            from_port=22,
            to_port=22
        },
        {
            from_port=6022,
            to_port=6022
        }
    ]
}
```

**For_EACH loop**
```
for_each =var.instances
instance_type= each.value
Name= each.key

varaibale "instances"{
    default={
        backend="t3.micro",
        frontend="t2.micro"
    }
}
```

**Provisioners**
- provisioners are used to take some action locally orremote when terraform servers are created-similar to userdata
- in local exec their is no need to connect to server but in remote we need to connect to server via connetion block
- generally provisioners will run only while creation of servers and when we add contion when=destroy,the provisioners run at destroy time
- when we destroy resources at that time the destroy provisioner will work
1. local exec - where terraform cmd is running
2. remote exec - inside the servers created by terraform
```
provisioner "local-exec"{
    when= "destroy"
    command="the server ip is $(self.public_ip)"
}
connection{
    type="ssh"
    user="ec2-user"
    password="DevOps321"
    host= self.public_ip //from our laptop it has to connect so we should give public ip only
}
provisioner "remote-exec"{
    inline=[
        "sudo-dnf install nginx -y",
        "sudo systemctl start nginx",
    ]
}
```