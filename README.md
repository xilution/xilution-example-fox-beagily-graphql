<h1 align="center" style="border-bottom: none;">xilution-graphql-backend-example</h1>
<p>
An example demonstrating how to build a GraphQL backend server using Xilution's IAM Suite (Elephant, Rhino, Hippo and Zebra), Beagily and Fox.
<p>
<p align="center">
  <a href="https://github.com/xilution/xilution-graphql-backend-example/issues">
    <img alt="Issues" src="https://img.shields.io/github/issues/xilution/xilution-graphql-backend-example.svg">
  </a>
  <a href="https://github.com/xilution/xilution-graphql-backend-example/network">
    <img alt="Forks" src="https://img.shields.io/github/forks/xilution/xilution-graphql-backend-example.svg">
  </a>
  <a href="https://github.com/xilution/xilution-graphql-backend-example/stargazers">
    <img alt="Stars" src="https://img.shields.io/github/stars/xilution/xilution-graphql-backend-example.svg">
  </a>
  <a href="https://github.com/xilution/xilution-graphql-backend-example/blob/master/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/xilution/xilution-graphql-backend-example.svg">
  </a>
</p>
<p align="center">
  <a href="https://travis-ci.org/xilution/xilution-graphql-backend-example">
    <img alt="Travis" src="https://img.shields.io/travis/xilution/xilution-graphql-backend-example.svg">
  </a>
</p>
<p align="center">
  <a href="https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fxilution%2Fxilution-graphql-backend-example">
    <img alt="Tweet" src="https://img.shields.io/twitter/url/https/github.com/xilution/xilution-graphql-backend-example.svg?style=social">
  </a>
</p>

## Use Case

TODO - Describe the use case

```text
             +------------------+
             | Xilution Account |
             +--------+---------+
                      |
                      v
               +------+-------+
               | Organization |
               +------+-------+
                      |
                      v
           +----------+----------+
           |    [ Elephant ]     |
           | Sub Organization(s) |
           +----------+----------+
                      |
                      v
      +--------------------------------+
      |               |                |
      v               v                v
+-----+-----+   +-----+-----+   +------+------+
| [ Hippo ] |   | [ Rhino ] |   |   [ Fox ]   |
| Client(s) |   |  User(s)  |   | Instance(s) |
+-----------+   +-----------+   +-------------+
```

TODO - explain this graph

* Xilution [Elephant](https://products.xilution.com/basics/elephant) is part of Xilution's IAM suite and is used to manage sub-organizations.
* Xilution [Hippo](https://products.xilution.com/basics/hippo) is part of Xilution's IAM suite and is used to manage sub-organization clients.
* Xilution [Rhino](https://products.xilution.com/basics/rhino) is part of Xilution's IAM suite and is used to manage sub-organization users.
* Xilution [Fox](https://products.xilution.com/integration/fox) is a managed API hosting solution that uses Docker to instantiate API server instances.

```text
                                        +-----------+
                                  +---->+ [ Zebra ] |
                                  |     |   Auth    |
                                  |     +-----------+
+-----------+     +---------+     |
|   User    +---->+ [ Fox ] +---->+
| Interface |     |   API   |     |
+-----------+     +---------+     |
                                  |    +--------------+
                                  +--->+ [ Beagily ]  |
                                       | Data Storage |
                                       +--------------+
```

TODO - explain this graph

* Xilution [Zebra](https://products.xilution.com/basics/zebra) is part of Xilution's IAM suite and is used to authenticate and authorize Rhino users and Hippo clients.
* Xilution [Beagily](https://products.xilution.com/basics/beagily) is a simple JSON data storage API that features integrated search and access control features.

## Features

TODO - add features

## Prerequisites

1. Install Docker Desktop: https://www.docker.com/products/docker-desktop
1. Install NVM: https://github.com/nvm-sh/nvm
1. Install Yarn: https://yarnpkg.com
1. Install jq: https://stedolan.github.io/jq/
1. Install cURL: https://curl.haxx.se/
1. Create a Xilution Account
    1. Open [https://prod.register.xilution.com](https://prod.register.xilution.com) to create a Xilution Prod account.
    1. Open [https://test.register.xilution.com](https://test.register.xilution.com) to create a Xilution Test account.
    
    * Note: Xilution Test and Prod accounts are not synchronized.

## General

### To Install Dependencies

1. Run `yarn install` to download dependencies.

### To Verify The Source Code

1. Run `yarn verify`.

## Set Up

### Environment Variables

1. Run `touch .env` to create a new environment variables file.
1. Run `echo "XILUTION_ENVIRONMENT={environment}" >> .env` to add your environment preference to the environment an variables file (.env).
    * {environment} is a Xilution environment. One of 'test' or 'prod'.

### Account Organization Authentication

1. Run `yarn xln:authentication:token-from-user-credentials`.
    * You will be prompted for your Xilution account username and password.
    * The access token saved to the environment variables file will expire in one hour.

### Account Organization Product Activation

Note: Requires Account Organization Authentication

1. Run `yarn xln:elephant:activate-for-account-organization`.
1. Run `yarn xln:hippo:activate-for-account-organization`.
1. Run `yarn xln:rhino:activate-for-account-organization`.

* Run `yarn xln:{product-name}:show-activation-for-account-organization` to see the status of an account organization's product activation.
    * {product-name} is one of `elephant`, `hippo` or `rhino`.
* Run `yarn xln:{product-name}:deactivate-for-account-organization` to deactivate a product for an account organization.

### Create a Xilution Sub-Organization

Note: Requires Account Organization Authentication

1. Run `yarn xln:elephant:create-sub-organization`.

* To see your sub-organizations, run `yarn xln:elephant:show-organizations`.
* To delete a sub-organization, run `yarn xln:elephant:delete-organization {sub-organization-id}`
    * {sub-organization-id} is a sub-organization id.

### Sub-Organization Product Activation

Note: Requires Account Organization Authentication

1. Run `yarn xln:zebra:activate-for-sub-organization`.
1. Run `yarn xln:beagily:activate-for-sub-organization`.
1. Run `yarn xln:fox:activate-for-sub-organization`.

* Run `yarn xln:{product-name}:show-activation-for-sub-organization` to see the status of a sub-organization's product activation.
    * {product-name} is one of `zebra`, `beagily` or `fox`.
* Run `yarn xln:{product-name}:deactivate-for-sub-organization` to deactivate a product for a sub-organization.

### Add an API User to the Sub-Organization

Note: Requires Account Organization Authentication

1. Run `yarn xln:rhino:sign-up-api-user {email} {username}`.
    * {email} is the new user's email address. Enter an email address that you have access to.
    * {username} is the new user's username.
    * A verification code will be emailed to the email address you entered when signing up the new user.
1. Run `yarn xln:rhino:verify-user-email {username} {code}` to verify the new user's email.
    * {username} is the new user's username.
    * {code} is the verification code the you received in your email inbox.

* To see the sub-organization's users run, `yarn xln:rhino:show-users`.
* To delete a sub-organization's user run, `yarn xln:rhino:delete-user {user-id}`.

TODO - make a note about needing a credit card in Prod.

### Add a Client to the Sub-Organization

Note: Requires Account Organization Authentication

1. Run `yarn xln:hippo:create-api-client`.

* To see the sub-organization's clients run, `yarn xln:hippo:show-clients`.
* To delete a sub-organization's client run, `yarn xln:hippo:delete-client {client-id}`.

### Sub-Organization Authentication

1. Run `yarn xln:zebra:token-from-api-client-credentials`.

### Prime Beagily with Some Data

Note: Requires Sub-Organization Authentication

1. Run `yarn xln:beagily:create-pet-type`.
1. Run `yarn xln:beagily:create-pet {name}` passing some different pet names to prime with Beagily data store with some data. 
   * {name} is a pet's name.

## Running Locally

1. Run `export $(grep -v '^#' .env | xargs)`.
    * Requires the Set Up step to be complete.
1. Run `yarn start`.
    * You can make changes to the source code and nodemon will automatically restart the server when the changes are saved.
    * Open `http://localhost:3123/health` in a browser to verify that the server is running.
    * Open `http://localhost:3123/graphql` in a browser to see the Apollo Playground.
        * Requires Authentication. See Example GraphQL Queries and Mutations / Authentication below.
    * `Ctrl-c` to stop.

## Example GraphQL Queries and Mutations

You can use variants of the following queries to test your API in the Apollo Playground.

### Authentication

For each of the following queries and mutations, you'll need to include the following header.

```json
{
  "Authorization": "Bearer {xilution-api-access-token}"
}
```

1. Run `yarn xln:zebra:token-from-api-client-credentials` to regenerate an API access token.

1. Run `cat .env | grep XILUTION_API_ACCESS_TOKEN` to see the access token you just generated. You'll need this when you make requests to the API's `graphql` endpoint.
    * Replace `{xilution-api-access-token}` in the JSON snippet above.

### List Pets

**Query**
```graphql
query Pets($sort: String, $query: String, $pageNumber: Int, $pageSize: Int) {
  pets(sort: $sort, query: $query, pageNumber: $pageNumber, pageSize: $pageSize) {
    data: content {
      id
      name
      createdAt
      owningUserId
    }
    total: totalElements
  }
}
```

**Variables**
```json
{
	"pageNumber": 0,
	"pageSize": 10
}
```

### Get Pet

**Query**
```graphql
query Pets($id: String!) {
  pet(id: $id) {
    id
    name
    createdAt
    owningUserId
  }
}
```

**Variables**
```json
{
	"id": "{pet-id}"
}
```

### Delete Pet

**Mutation**
```graphql
mutation Pets($id: String!) {
  deletePet(id: $id) {
    id
  }
}
```

**Variables**
```json
{
	"id": "{pet-id}"
}
```

### Create Pet

**Mutation**
```graphql
mutation Pets($newPet: NewPet!) {
  createPet(pet: $newPet) {
      id
      name
      createdAt
      owningUserId
  }
}
```

**Variables**
```json
{
	"newPet": {
		"name": "{name}",
		"owningUserId": "{owning-user-id}"
	}
}
```

### Update Pet

**Mutation**
```graphql
mutation Pets($id: String! $updatedPet: UpdatedPet!) {
  updatePet(id: $id pet: $updatedPet) {
      id
      name
      createdAt
      owningUserId
  }
}
```

**Variables**
```json
{
	"id": "{pet-id}",
	"updatedPet": {
		"name": "{name}"
	}
}
```

## Docker

### To build the Docker image

This tags your docker image as `xilution-graphql-backend-example`.

1. Run `yarn docker:build`.

### To run the Docker image locally

1. Run `yarn docker:start`.
    * Open `http://localhost/health` to verify that the server is running.
    * Because the Docker image was build in production mode, the Apollo Playground is not available.
    * The GraphQL endpoint can by accessed at `http://localhost/graphql`.

### To stop the Docker image

1. Run `yarn docker:stop`.

### To publish the Docker image to Docker Hub

You'll need a [Docker Hub](https://hub.docker.com/) account to execute the following.

1. Run `yarn docker:publish` to push the image to your Docker Hub account.

## Xilution Fox

Fox can pull a Docker image from your Docker Hub account.
To grant Fox pull access the Docker image, either make the image public or add `tbrunia` as a [collaborator](https://docs-stage.docker.com/v17.12/docker-hub/repos/#collaborators-and-their-role).

### Create a Fox Instance

A Fox Instance contains data that instructs Fox on how to run your Docker image.
You provision a Fox Instance to start your API.
Likewise, you deprovision a Fox Instance to stop your API.

1. Run `yarn xln:fox:create-instance`.

* To see your instances, run `yarn xln:fox:show-instances`.
* To delete a instance, run `yarn xln:fox:delete-instance {instance-id}`.

### Provision the Fox Instance

1. Run `yarn xln:provision-fox-instance`, to provision the Fox instance.
1. Run `yarn xln:show-fox-instance-status`, to see the status of your Fox instance.
    * It can take up to 5 minutes to fully provision your Fox instance.
    * Provisioning is complete when you see the following.
        ```json
        {
           "status": "CREATE_COMPLETE"
        }
       ```
    * Now you can access the GraphQL Example running on Fox.

### Access The GraphQL Example Running on Fox

1. Run `cat .env | grep XILUTION_INSTANCE_ID` to see your Fox Instance ID.
1. Open `https://{instance-id}.prod.fox.integration.xilution/health` in a browser to verify that the server is running.

The Apollo Playground is not available when running in Fox because the Docker image was build in production mode, 
1. The GraphQL endpoint can by accessed at `https://{your-fox-instance-id}.prod.fox.integration.xilution/graphql`.

### Restart the Fox Instance

You can make changes to your API, build and redeploy using the following commands.

1. Run `yarn docker:build`.
1. Run `yarn docker:publish` to push the image to your Docker Hub account.
1. Run `yarn xln:fox:restart-instance`, to restart the instance in the Fox managed API hosting service.

We recommend adding a version endpoint to your API and use it to determine when a new version of your API has been deployed.

### Deprovision the Fox Instance

1. Run `yarn xln:fox:deprovision-instance`, to deprovision the Fox instance.
1. Run `yarn xln:fox:show-instance-status`, to see the status of your Fox instance.
    * It can take up to 5 minutes to fully deprovision your Fox instance.
    * Deprovisioning is complete when you see the following.
        ```json
        {
           "status": "NOT_FOUND"
        }
       ```

### Delete the Fox Instance

1. Run `yarn xln:fox:delete-instance {instance-id}`, to delete the Fox instance.

---
Copyright 2019 Teapot, LLC.  
Xilution is a DBA of Teapot, LLC.
