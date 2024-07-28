# tofu
- Documentation around OpenTofu

## Tofu Conventions
| File name       | Purpose |
| :--------       | :------- |
| main.tf         | Main configuration file containing resource definition
| variables.tf    | Contains variable declarations
| outputs.tf      | Contains outputs from resources
| provider.tf     | Contains Provider definition
| opentofu.tf     | Configures OpenTofu behavior

## Variables (Env vars)
- Setting the values to nothing and then it will prompt the users to input values at apply time

### Usage of variables
```tf
resource "local_sensitive_file" "secret" {
	filename = "${var.filename}"
	content = "this secret goes here"
}
```

### Environment Variables
```bash
export TF_VAR_variable_name="value"
export TF_VAR_filename="/tmp/file.txt"

tofu apply
```

### .tfvars
- make use of .tfvars to pass in senstive values
```
variable_name="value"
filename="/tmp/file.txt"
```

### Variable Definition Precedence
- The last (bottom of the list) takes highest Priority (the following table says in what order it goes in)
| Order | Option | 
| :---: | :----- |
| 1     | Environment Variables |
| 2     | terraform.tfvars |
| 3     | *.auto.tfvars (alphabetical order) |
| 4     | `-var` or `-var-file` (command-line flags) |

### Variable Block
```
variable "instance_type" {
	default = "e2.medium"
	description = "size of compute machine"
	type = string
	sensitive = <boolean(true|false)>
}

# Variable Validation
variable "ami" {
	type = string
	description = "The id of the machine image (AMI) to use for the server"
	validation {
		condition = substr(var.ami, 0, 4) == "ami-"
		error_message = "The AMI should start with \"ami-\"."
	}
}

```

### Types in OpenTofu
Values that OpenTofu is allowed to express are the following:
- string
- number
- bool
- list
- set
- map
- null

*Examples*
```tf
# list
variable "colors" {
	default = ["blue", "green", "red"]
	type = list
}
# --> usage: var.colors[0]
# note: can change type to be more specific: `list(string)`

# map
variable "wordcount" {
	type = map
	default = {
		"book" = "long"
		"song" = "medium"
		"poem" = "short"
	}
}
# --> usage: var.colors["book"]
# note: can change type to be more specific: `map(string)`


# objects
variable "pet" {
	type = object({
		name = string
		color = string
		age = number
		food = list(string)
		favorite_pet = bool
	})
	
	default = {
		name = "greg"
		color = "gray"
		age = 4
		food = ["fish", "chicken", "socks"]
		favorite_pet = true
	}
}


# tuples
variable web {
	type = tuple([string, number, bool])
	default = ["web1", 5, true]
}

```


- Reference: https://opentofu.org/docs/language/expressions/types/
