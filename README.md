# ib-terraform

Terraform → IaC tool, declarative, multi-cloud.
Providers → plugins for cloud services.
State file → tracks infra.
Plan vs Apply → dry run vs execution.
Modules → reusable code.
Init → project bootstrap.
Variables → input/output for reusability.
Refresh vs Taint → update state vs force re-create.
Fmt & Validate → formatting & validation.

Terraform's type system includes primitive types such as string, number, bool, and more complex types like lists, maps, and objects. Here's a brief overview of some of the main types in Terraform:

1. 	Primitive Types: These include basic data types like string, number, and bool. They represent single values.
2. 	Lists and Tuples: Lists (list) represent ordered collections of elements, while tuples (tuple) represent fixed-size collections of elements of different types.
3. 	Maps: Maps (map) represent collections of key-value pairs, where each key is associated with a value.
4. 	Objects: Terraform also supports complex types that can represent objects with multiple attributes. These can be represented using a combination of maps and lists.
5. 	Any Type (any): The any type allows for flexibility in defining variables that can hold values of any type.

Terraform Provider :- a provider is a plugin that lets Terraform interact with cloud providers, SaaS APIs, or other platforms(like docker, kubernetes etc). 
terraform syntax :- 
terraform { 
required_providers
 {
 aws = {
    source = "hashicorp/aws" 
     version = "~> 6.0" 
      }
   }
}

resource <resource_type> <resource_name> {
ami      = "ami-123456"
  instance_type = "t2.micro"
}
Example:-
resource "aws_instance" "east_server" {
  provider = aws.us_east
  ami      = "ami-123456"
  instance_type = "t2.micro"
}

terraform init :- For Initialization like install dependency and plugin etc
terraform validate :- Ensure applied changes meet defined policies.
terraform plan :- It will show the Plan that what thing your terraform file will change like “+” sign means Add  “–“ sign means delete or “~” means update.
terraform apply :- Final phase on provider end required changes.
terraform destroy :- Safely decommission resources when necessary.
terraform destroy -target <target_name> It will destroy only targeted resource.
terraform show :- it will show .tfstate file.
terraform refresh :- It will refresh the code like whatever you changes manually on infra it will update in code( tfstate file) also.
terraform console :- Open terraform console.
terraform fmt :- It will arrange your code in terraform code format.
dynamic blocks :- Dynamic blocks in Terraform allow you to generate multiple nested blocks dynamically based on data structures like lists, maps, or sets. They provide a way to handle dynamic configurations where the number or structure of nested blocks isn't known until runtime. This feature enhances the flexibility and expressiveness of Terraform configurations.
terraform taint :- taint file is recreated because we told to terraform interpreter that it this file is taint so we have to recreate it. 
Note :- deprecated now.
terraform import: Imports existing infrastructure into Terraform state.
Terraform provisioner :- are used for executing scripts or shell commands on a local or remote machine as part of resource creation/deletion.
·       File Provisioner: Used to copy files or directories to the remote machine.
·       Remote-Exec Provisioner: Allows executing commands on the remote machine over SSH or WinRM.
·       Local-Exec Provisioner: Executes commands on the machine where Terraform is run. This is typically used for local tasks or for calling external scripts.
 
*Terraform state list command is used to list all the resources Terraform is currently managing in your state file (terraform.tfstate). 
Terraform graph :- It will show graphical representation of flow.
 
Terraform Workspace:-
Terraform workspace list :- show list of workspaces
Terraform workspace show :- Display info about current selected workspace
Terraform workspace new <name> :-
Terraform workspace select <environment> :- For change environment.
Terraform workspace delete <name>
By Default one workspace is created and apart from this you can create as much workspace you want like you can create dev and prod workspace.
All workspace have different state file.
Terraform module:- Terraform module is a container for multiple resources that are used together. It allows you to encapsulate and reuse infrastructure configurations, making your Terraform code more modular, maintainable, and shareable.
Terraform Registry:- The Terraform Registry is the official public repository where HashiCorp and the community publish Terraform providers and modules.  
URL: https://registry.terraform.io 

Terraform backend :- In Terraform, the term "backend" refers to the method and location where Terraform stores its state file, which contains the current state of your infrastructure
Loki mechanism.
Debugging Terraform
Terraform has detailed logs that you can enable by setting the TF_LOG environment variable to any value. Enabling this setting causes detailed logs to appear on stderr.
You can set TF_LOG to one of the log levels (in order of decreasing verbosity) TRACE, DEBUG, INFO, WARN or ERROR to change the verbosity of the logs.
Setting TF_LOG to JSON outputs logs at the TRACE level or higher, and uses a parseable JSON encoding as the formatting.
Warning: The JSON encoding of log files is not considered a stable interface. It may change at any time, without warning. It is meant to support tooling that will be forthcoming, and that tooling is the only supported way to interact with JSON formatted logs.
Logging can be enabled separately for Terraform itself and the provider plugins using the TF_LOG_CORE or TF_LOG_PROVIDER environment variables. These take the same level arguments as TF_LOG, but only activate a subset of the logs.
To persist logged output you can set TF_LOG_PATH in order to force the log to always be appended to a specific file when logging is enabled. Note that even when TF_LOG_PATH is set, TF_LOG must be set in order for any logging to be enabled.
If you find a bug with Terraform, please include the detailed log by using a service such as gist.

