# Poseidon Data Adapter project

You can create a Poseidon Data Adapter project using the Yeoman generator **yo @kognifai/poseidon:dataadapter**.  **Yeoman** is a bootstrapping tool, which can be used to scaffold a Poseidon Data Adapter solution.  For more information, please visit http://yeoman.io.  This generator once generated has an interface as well as sample application projects.

# Install Yeoman

We can install Yeoman if it is not already installed:
```javascript
npm install -g yo
```

For more details, look into the Yeoman's Getting Started page: http://yeoman.io/learning/index.html 

Install this generator,
```typescript
npm install -g @kognifai/generator-poseidon
```
To ensure that this generator is successfully installed, we can use the below command.  This would list all the available generators along with other useful **yo** commands.

```typescript
yo --help
```
 ![image.png](.%20images/image-b5b30524-38c5-48a0-826c-220abd294f64.png)

# Create a Poseidon Data Adapter Solution

Now that we have Yeoman and the Poseidon generator installed, we can use the sub-generator to scaffold our solution.

**Note**:  Remember to call this Yeoman generator in an empty directory.
```typescript
mkdir D:\_WorkArea\DataAdapter
cd D:\_WorkArea\DataAdapter
```
Once the directory is created and we are in it,
```typescript
yo @kognifai/poseidon:dataadapter
```

Upon running the above command, we would be required to provide a data adapter project name as well as a Docker image name.

  ![image.png](.%20images/image-214e8b82-1a2a-43bb-8730-a19d2f541efa.png)

Once it is successfully created, we should see a project setup similar to the image as below:

 ![image.png](.%20images/image-a7c43374-d0b3-4a2a-8eb4-2a4b98e05b63.png)

# Registering our custom data adapter
We need a registration tool for registration.
```typescript
npm install -g @kognifai/poseidon-app-registration-cli@">=2.0.0-beta.1 <3.0.0"
```
Once we have the above tool installed, we can do the registration.
```typescript
poseidon-app-registration-cli --dataadaptermanifest mydataadapter\dataadapter.manifest.json --username  xyz --password xyz
```
Parameter **--dataadaptermanifest** - it is the path to **dataadapter.manifest.json** file, which is in the above ASPDOTNET Data Adapter project scaffolded above.


