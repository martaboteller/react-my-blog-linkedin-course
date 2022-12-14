<!-- PROJECT TITLE -->
<br />
<div align="center">
<img src="https://avatars.githubusercontent.com/u/43497073?s=400&u=76b8ae73d9487edc8c80e987e9067832446ab6d1&v=4" alt="Marta Boteller" width="80" height="80">
<h2 align="center">MERN STACK</h3>
<p align="center"> This is a simple MERN web project</p>
<br />
</div>
<br/>

## About the project

In order to achieve a broader knowledge in tech stacks I've created this simple project that combines the use of M. MongoDB, E. Express, R. React, N. Node.js.

Here's why -> :rocket: [go fullstack!](https://martaboteller.com/fullstack)

<br/><br/>

## Description

<img style="aign:center" src="./utils/ui.png" width="400" alt="project's view">

<h5>Following the <a href="https://www.linkedin.com/learning/react-creating-and-hosting-a-full-stack-site/react-for-full-stack-solutions?autoplay=true&contextUrn=urn%3Ali%3AlyndaLearningPath%3A593715e0498e9e9be7fb8506">Shaun Wassell's Linkedin course</a> I've created a website blog. It has three pages. We've learned how to create an interface made with React components, develop a Node.js server and tie in a MongoDB database.</h5>

<br/><br/>

## Built with

Major frameworks/libraries used:

  <img style="align:left;border:solid;border-color:black;margin:2px" src="https://brandslogos.com/wp-content/uploads/images/large/mongodb-logo-black-and-white.png" height="50" width="180"/>

  <img style="align:left;border:solid;border-color:black;margin:2px;" src="https://rithmapp.s3-us-west-2.amazonaws.com/assets/express-logo.png" height="50" width="180"/>

  <img style="align:left;border:solid;border-color:black;margin:2px" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTpm1LELjmkTPuaSpxXVh012-vkwBwpGaKUQ6WwYNdVmxPS1W0FJyN2tA1JwuJmo_Td0Kg&usqp=CAU" height="50" width="180"/>

  <img style="align:left;border:solid;border-color:black;margin:2px" src="https://brandslogos.com/wp-content/uploads/images/large/nodejs-logo-black-and-white.png" height="50" width="180"/>
  
<br/><br/>

## What's included

I've been working with two main folders: frontend & backdend.

The structure of the frontend is as follows:

```
my-blog/
????????? src/
    ???????????? components/
    ???   ????????? AddCommentForm.js
    ???   ????????? ArticlesList.js
    ???   ????????? CommentsList.js
    ???   ????????? UpvotesSection.js
    ???????????? pages/
    ???   ????????? AboutPage.js
    ???   ????????? article-content.js
    ???   ????????? ArticleListPage.js
    ???   ????????? HomePage.js
    ???   ????????? NotFoundPage.js
    ????????? App.css
    ????????? App.js
    ????????? index.css
    ????????? index.js
    ??????  Navbar.js
```

The structure of the backend is as follows:

```
my-blog-backend/
????????? src/
????????? build/
????????? server.js
????????? utils/
```

<br/><br/>

## Connecting front-end with back-end

1. Install CORS
2. Add the proxy property at package.json

```javascript
"proxy": http://localhost:8000"
```

3. Delete first part of fetch commands

```javascript
const result = await fetch(`/api/articles/${articleName}/add-comment`, {
      method: 'post',
      body: JSON.stringify({ username: name, text: comment }),
      headers: {
        'Content-Type': 'application/json',
      },
```

<br/><br/>

## Preparing the app for release

1. Change my-blog/public/index.html
   ```html
   <title>My Blog</title>
   ```
2. Change my-blog/public/manifest.json
   ```javascript
   "short_name": "My Blog",
   "name": "My Blog - Following Linkedin Tutorial",
   ```
3. Build the project
   ```
   npm run build
   ```
4. Copy the created folder to my-blog-backend/src/build
5. In server.js add
   ```javascript
   import path from 'path';
   app.use(express.static(path.join(__dirname,'/build')));
   app.get('*', (req,res)=>{res.sendFile(path.join(__dirname + '/build/index.html))});
   ```

<br/><br/>

## AWS Deployment

<br/>
<h4>Creating and SSHing into AWS instance</h4>

1. Log into AWS Management Console
2. Select EC2
3. Select Launch Instance and Amazon Linux 2 AMI
4. Leave it with the defaults, Review and Launch, then Launch.
5. Create a new key pair, providing a name, i.e my-blog-key. This will download a .pem file
6. Open a terminal and move the downloaded file into .ssh folder
7. At AWS site select the running instance and copy the public DNS address. Provide permissions and connect:
   ```
   chnod 400 /.ssh/my-blog-key.pem
   ssh -i /.ssh/my-blog-key.em ec2-user@[copied public dns]
   ```

<h4>Setting up an AWS instance</h4>

1. Install git

   ```
   sudo yum install git
   ```

2. Install nvm

   ```
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
   ```

   ```
     . ~/.nvm/nvm.sh
   ```

   ```
   nvm install --lts
   ```

3. Install npm
   ```
   npm install -g npm@latest
   ```
4. Install Mongodb

   ```
   sudo nano /etc/yum.repos.d/mongodb-org-6.0.repo
   ```

   Copy content of this [site](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-amazon/#install-mongodb-community-edition) to the doc.

   ```
   sudo yum install -y mongodb-org
   ```

5. Start Mongodb and create database
   ```
   sudo service mongod start
   ```
   ```
   mongo
   ```
   ```
   use my-blog
   db.articles.insert([
     {
       name:'learn-react',
       upvotes:0,
       comments:[],
     },{
       name:'learn-node',
       upvotes:0,
       comments:[],
     },{
       name:'my-tougths-on-resumes',
       upvotes:0,
       comments:[],
     }
   ])
   ```

<br/>

<h4>Running a full-stack app on AWS</h4>

1. Copy the github clone url of the repo
2. At AWS terminal:
   ```
   git clone [the copied address]
   ```
   ```
   cd my blog
   ```
   ```
   npm install
   ```
3. Install Forever package to keep server running
   ```
   npm install -g forever
   ```
   ```
   forever start -c "npm start" .
   ```
   ###### Shows the port where is running:
   ```
   forever list
   ```
   ```
   sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8000
   ```
4. Select the runnning instance at AWS. Edit the security group at Inbound tab. Add rule, http, from source 'anywhere' and save it.

5. App runnning at the DNS public address!

<br/><br/>

## Roadmap

- [x] Configure with local MongoDB database
- [x] Configure with atlas MongoDB database
- [x] Form validation check
- [x] Amazon Web Services (AWS) deployment
- [ ] Resposive frontend

<br/>

## Author

I'm Marta Boteller, little more about me at my [website](https://martaboteller.com).
<br/> <br/>

## Acknowledgments

<p>The Linkedin course is outdated I would like to thank William Hamilton and his  <a href="https://www.youtube.com/user/Draxy1980">Youtube channel</a>. He has created a video series in order to complete the course with the newer libraries still following along with Shaun's course.</p>

Please also find Shaun Wassell's course: [React: Creating and Hosting a Full-Stack Site](https://www.linkedin.com/learning/react-creating-and-hosting-a-full-stack-site/react-for-full-stack-solutions?autoplay=true&contextUrn=urn%3Ali%3AlyndaLearningPath%3A593715e0498e9e9be7fb8506)
