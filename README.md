# Terraform offline for Windows user

## Initialize Terraform offline with the Filesystem mirror

Run Terraform init without an internet connection for Ubuntu users, we can run the command through the cache from terraform.rc file. 

## Step 1: 
Create a directory in your system. 
```
mkdir "$HOME/cache_tf"
```
Now simply copy the registry.terraform.io folder here. This configuration helps you to run terraform init without an internet connection

## Step 2: 
Create this file inside the above directory. Create "terraform.rc".

```
provider_installation {
  filesystem_mirror {
    path = "/home/{user}/cache_tf"
    include = ["registry.terraform.io/hashicorp/*"]
  }
  direct {
    exclude = ["registry.terraform.io/hashicorp/*"]
  }
}
plugin_cache_dir = "home/{user}/cache_tf"
disable_checkpoint=true
```

## Step 3: 
Setup env variables as follows
  
  ```
for Ubuntu
export TF_PLUGIN_CACHE_DIR="c:/cache_tf"
export TF_CLI_CONFIG_FILE="c:/cache_tf/terraform.rc"
  ```

## Step 4: 
Now just run 
```
terraform init
  ```
It will take the cache from the registry.terraform.io in the cache_tf directory


