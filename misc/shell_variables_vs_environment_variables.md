#### Shell variables vs Environment variables
  
  ```bash
  ## Environment variables
  export HOST=www.example.com  ##  Defining a variable with export
  printenv | grep HOST         ## HOST=www.example.com
  echo $HOST                   ## www.example.com
  
  ## Shell variables:
  PORT=443                     ## Defining a variable without export
  printenv | grep PORT         ## prints nothing
  echo $PORT                   ## 443

  sh                           ## create a new child process
  echo $HOST                   ## www.example.com
  echo $PORT                   ## prints nothing
  ## environment variables are propogating to child process and the shell variables are not.
  ```