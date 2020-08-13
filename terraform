provider "aws" {

  access_key = "AKIAJ4EAROPMZ635FGOQ"

  secret_key = "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"

  region = "ap-south-1"

}

 

resource "aws_instance" "terraform_webserver" {

  ami = "ami-0ce933e2ae91880d3"

  instance_type = "t2.micro"

  key_name = "tf_key"

provisioner "file"{
source = "myscript.sh"
destination = "/tmp/myscript.sh"
}

provisioner "remote-exec" {
    inline = [
      "sudo chmod 777 /tmp/myscript.sh",
       "sh /tmp/myscript.sh",
"sudo chmod 777 -R /var/www/html",
]
 }

provisioner "file"{
source = "index.html"
destination = "/var/www/html/index.html"
}


  connection {
   host = "${self.public_ip}"

    user = "ec2-user"

    private_key = "${file("tf_key.pem")}"

  }

}
