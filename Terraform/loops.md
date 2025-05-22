**LOOPS**
1. count based loop  - iterate over list type of variables
2. for each loops
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
- Terraform has one state file ,in that all the changes which we do from code are noted and it compares to actula infro in provider,if any one changes from provider side it will pick again from statefile and modify the changes
