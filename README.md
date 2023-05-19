# githubActionsSecurity

## script injection

- add to the issue this script a you can letter to replace the title in shell command put code in double bracets is optional put the then you will see this new command injection in your action
  - a";echo get your secrets"
- to solve this issue it is better to add env key word then add inside it tittle varable and add to it value of the title in run command only use title variable

## permissions

- you can add it to the whole workflow or for the certain permission
- add keyword permissions inside your job you can write value to it directly writeall or read all but it is better to have inside permission keyword your action in our example issue and give to it a value read or write
- if you add one permission to a job other permission by default are disabled

## github token

- secrets.GITHUB.TOKEN
  - it generated automaticially by github
  - because this request to github api must be authenticated
  - this token availble in our job and it will be valid untill our job done
  - the scopr of this token can be set with permissions
  - generally we used this token a lot when we check for our steps using certain action github using its token here if i using permission read so it will not be working
  - if you want to restrict the primitive behaviour of github token go to your repsitory setting under action then general then you can change the workflows permissions
  - you have here other setting
    - allow or not github actions to create and approve pull request
    - pull request comes from fork
    - \*ctions permissions

## openIdConnect

- dynamicially get permission for exactly what we need to do from a third party when we need to do that in other words githubaction workflow dynamically request a permission a third party providerand then this permission is granted if everything has been set uo correctly but only valid for a short period of time and it is restricted to the kind of action that must be performed
- how to add it:
  - example AWS
  - add openIdConnect to a service called IAM
  - in this service in dashboard under identity provider click on add provider
  - here choose opnIdConnnect
  - under url and audience get them from githubactions docmentation
  - click getthumbprint
  - noe provider added
  - now in AWS should define kind of permission should github request
  - for that we should assign a role for our provider
  - click on ou provider then in the top right corner click on assign role
  - her you cann add new one or using exisiting one
    - a role is a docuemt which describe a permission that will be added to an entity
  - here select web entity then add same url and audience you have entred before
  - select the appropriate policy or create new one next then skip tag
  - then give this role a name then create it
  - click on rile you may see the tap trust relationship you can change it to be mor restictive
  - now go to github action or your workflow
  - delete env varaible you do not need them any more
  - add another step using action created by AWS this actions is
  - aws-actions/configure-aws-credentials@v3
  - then add kexword with inside it add role-to-assume then add arn value in your role in AWS and add aws-region key
  - you should add some permission to your job because by default idtoken permission is alwasy disabled and we need it to talk to AWS so in our example add inside deploy job keyword permissions inside it add id-token: write and content: read
