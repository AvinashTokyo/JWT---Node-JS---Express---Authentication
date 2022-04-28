# JWT---Node-JS---Express---Authentication

//laith harb - JWT Authentication with Node 
1. npm init -y --> create a package.json.

2. nodemon is for reload our server
    - npm install nodemon -g

3. in package.json --> 
    - "scripts": {
    "start": "nodemon index.js"
  },

4. Create a index.js File.

5. npm install express 

6. Add Basic Code 
    - const express = require('express');
    - const app = express();
    - app.listen ( 5000 , () => {
        console.log("Now Running on port 5000");
    });

7. npm run start
    - this will start [nodemon];

8. SignUp Flow -->
    - User Provides an Email & Password 
        - Validate Email & Password
            - Validate if User with that Email doesn't Already Exist
                - Hash the Password
                    -  Save User to DB
                        - Send a JWT

9. For multiple routes
    - create a folder named routes
        - inside it create auth.js

10. In auth.js
    - const router = require('express').Router();
    - module.exports = router;
    - router.get('/' , ( req, res ) => {
    res.send('Auth Get Router Working');
})

11. in index.js
    - //accessing all the routes from auth.js file
    - app.use(express.json());
    - app.use('/auth' , auth);

12. Install express validator for validate email and password.
    - npm install express-validator

13. With use of Express-validators --> 

                router.post(
                "/signup",
                [
                    check("email", "Please Provide a valid Email - abc@mail.com").isEmail(),
                    check("password", "Password must be of length 6").isLength({
                    min: 6,
                    }),
                ],
                (req, res) => {
                    const { password, email } = req.body;

                    //  VALIDATED THE INPUT
                    const errors = validationResult(req);

                    if(!errors.isEmpty()){
                        return res.status(400).json({
                            errors: errors.array()
                        })
                    }

                    //VALIDATE IF USER DOESN'T ALREADY EXISTS
                    let user = users.find((user) => {
                        return user.email === email
                    });

                    if(user){
                        res.status(400).json({
                            "errors": [{
                                "msg": "This user already exists"
                            }]
                        })
                    }



                    
                    // console.log(password, email);
                    // res.send("Auth Route Working");
                    res.send("Validation Passed, Signup Success");
                }
                );

14. created a db.js file having all the users details.

                    const users = [
                    {
                        email: "avi@mail.com",
                        password: "123456"
                    }
                ];

                module.exports = {
                    users
                }

15. Hasing the password
    - in npm we have a package to hash the password --> node.bcrypt.js
    - npm install bcrypt
    - check in the package.json -> 
                    "dependencies": {
                    "bcrypt": "^5.0.1",
                    "express": "^4.18.0",
                    "express-validator": "^6.14.0"
                }

16. JWT - json web token  - contains who the client is
    - npm install jsonwebtoken






