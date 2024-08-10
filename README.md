# Cross-site Request Forgery
This project demonstrates a _Cross-Site Request Forgery (CSRF)_ attack on a fictional social networking site, _Social Network DevNet_. The attack exploits a vulnerability in the site that allows unauthorized state-changing requests to be made on behalf of authenticated users without their explicit consent.

## Project structure
In this project, several files work together to simulate and demonstrate the process and impact of a Cross-Site Request Forgery (CSRF) attack on a fictional social networking site called _Social Network DevNet_. The key components of this project are as follows:

```
Cross-site Request Forgery Project
│   README.md
│   all_posts.txt
│   index.js
│   package-lock.json
│   package.json
│
└───views
│   │   devnet_error.html
│   │   devnet_success.html
│   │   login.html
│   │   shocking_message.html
│   │   social_network_devnet.html
```

- `all_posts.txt`: This file contains all posts made by a user on the _Social Network DevNet_. It serves as a repository to log user activity and content.
- `index.js`: This script implements the server functionality, processing multiple requests from users. It handles operations such as serving webpages, processing login requests, and handling post submissions.
- `social_network_devnet.html`: This is the main webpage for developers, called _Social Network DevNet_. It is the primary interface where users post updates, and view content.
- `devnet_error.html`: This webpage displays an "Invalid token" error message to unauthorized users. It is used to inform users of authentication and authorization failures.
- `devnet_success.html`: This webpage confirms the successful addition of a new post to the _Social Network DevNet_. It provides users with positive feedback upon the successful completion of their actions.
- `login.html`: This is the login page where users authenticate themselves to gain access to their accounts on _Social Network DevNet_.
- `shocking_message.html`: This webpage presents a shocking message designed to entice and increase user curiosity. It is part of the social engineering tactic used in the CSRF attack scenario to lure users into clicking a malicious link.

Together, these files demonstrate how a CSRF attack can exploit vulnerabilities in web applications, leading to unauthorized actions being performed on behalf of unsuspecting users.

## Presenting the CSRF Attack
For a comprehensive understanding of the background and demonstration, please refer to the [loop page](https://uniquify0.sharepoint.com/:fl:/g/contentstorage/CSP_cce23060-774c-4565-8c87-4156d1594499/ER0NptlTpLlBgM2LPMXNldEBQOUhkokuGeDQr6BGulww_g?e=FUxjUE&nav=cz0lMkZjb250ZW50c3RvcmFnZSUyRkNTUF9jY2UyMzA2MC03NzRjLTQ1NjUtOGM4Ny00MTU2ZDE1OTQ0OTkmZD1iJTIxWUREaXpFeDNaVVdNaDBGVzBWbEVtZWg3WmNSS1AtNUFra0xhaHRlWlU0MlpEbUJSa1Z1WlJvbVUya1g4OEl0XyZmPTAxVU1DUEZMSTVCV1ROU1U1RVhGQVlCVE1MSFRDNDNGT1ImYz0lMkYmYT1Mb29wQXBwJnA9JTQwZmx1aWR4JTJGbG9vcC1wYWdlLWNvbnRhaW5lciZ4PSU3QiUyMnclMjIlM0ElMjJUMFJUVUh4MWJtbHhkV2xtZVRBdWMyaGhjbVZ3YjJsdWRDNWpiMjE4WWlGWlJFUnBla1Y0TTFwVlYwMW9NRVpYTUZac1JXMWxhRGRhWTFKTFVDMDFRV3RyVEdGb2RHVmFWVFF5V2tSdFFsSnJWblZhVW05dFZUSnJXRGc0U1hSZmZEQXhWVTFEVUVaTVR6WTJSa2hWUlVSTlNqUmFRa3hKUWxsT1VGUkxXa2xGVmpNJTNEJTIyJTJDJTIyaSUyMiUzQSUyMjNiOTg1MWU2LTI4YzMtNGY0YS1iNWYxLWQ5YzEzZDBkMDM3ZiUyMiU3RA%3D%3D) in the Demo section.

### Install necessary libraries
Before starting the attack, you need to install the necessary libraries. Use the following command to install the required packages:

```
npm i
```

I have prepared a `package.json` file, so running the above command will automatically install all necessary packages.

Next, open the `index.js` file and set the `PROTECT_CSRF` variable to `false` to disable CSRF protection before proceeding with the attack on the prepared website.

### Opening the _Social Network DevNet_ Website
To open the _Social Network DevNet_ website, start by running the following command to initiate the server:

```
node index.js
```

After starting the server, open your browser and navigate to `http://localhost:3000`. The website requires users to log in before posting a new message. A default account is provided with the username `root` and password `root`.

![Login page](/demo_images/login_page.png)

Once successfully logged in, users can use _Social Network DevNet_ to post new messages. On this page, you will see:
- A form on the left-hand side to post new messages to Social Network DevNet.
- A list of the user’s posts on the right-hand side.

![Social Network DevNet](/demo_images/social_network_devnet.png)

Now the user can write a new message and post them to the _DevNet_.

### Opening a Website Containing a Shocking Message
To view the shocking message, open the `shocking_message.html` file located in the `view` folder using your browser. This file displays a website with shocking content designed to entice curiosity.

![Shocking message site](/demo_images/shocking_message.png)

This website is publicly accessible and does not require an account for access.

### The Attack Execution
Driven by curiosity about the bizarre news, the root user decides to read the post and clicks the "Read more" button. As a result, a new post saying `This horse knows karate!` appears on his wall without his permission.

![Successfully attacked](/demo_images/attacked.png)

### Protecting the _Social Network DevNet_ Website
To mitigate CSRF attacks, I have included a variable called `PROTECT_CSRF`, which is set to `true` by default to protect the website.

When this variable is enabled, a hidden token is sent along with the form submission. This token is used to verify that the form is coming from the legitimate website.

After setting `PROTECT_CSRF` to `true` and repeating the previous steps, the website will return an error notification page instead of posting the message successfully.

![Invalid token](/demo_images/invalid_token.png)
