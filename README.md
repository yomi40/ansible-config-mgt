# ansible-config-mgt

provider "aws" { region = "eu-west-3" }

variable cidr_blocks { description = "cidr blocks and name tags for vpc and subnets" type = list(object({ cidr_block = string name = string })) }

variable avail_zone { default = "eu-west-3a" }

<!-- Demo on Github -->
resource "aws_vpc" "myapp-vpc" { cidr_block = var.cidr_blocks[0].cidr_block tags = { Name = var.cidr_blocks[0].name } }

resource "aws_subnet" "myapp-subnet-1" { vpc_id = aws_vpc.myapp-vpc.id cidr_block = var.cidr_blocks[1].cidr_block availability_zone = var.avail_zone tags = { Name = var.cidr_blocks[1].name } }

<<-- Demo on Github webhook -->>
