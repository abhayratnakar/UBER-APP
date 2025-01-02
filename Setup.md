* Full Steps of my code.

*******Full Setup of before project*******
1) app.js
    -> Create app.js file and require express and create "/" route in that and export that
    -> import dotenv to store all personal details and use cors to achieve cors policy.
2) server..js
    -> Now it's time to create server, require http and user createServer method and give that our exported app and make our server to listen on a perticular port useing listen function

3) Database :- Db/Db.js
    -> Now Create a folder Db which stores all database related files and folders then create Db.js in that
    -> require mongoose and use and create a simple function to connect our mongoose with project using connect function of mongoose now export that function for Ex conntectToDb();
    -> now import it in our app.js and call this function there. 

*******Register Functionality's*******
4) model setup :- Create models folder
    1) user.model.js
       ->  Now create user.model.js and create one include all the properties and functionality that userModel can have.
       -> require mongoose and user Schema of that to create Schema and in that schema mention all the properties which user can have.
       -> use model function of mongoose to create a model give your scema to that function and give a perticular keyword and then export that model.

5)  Services setup :- Create services folder
    1) user.service.js
        -> Now create user.service.js to write all Services related to user in that file
        -> Add first service to check that all fields are user giving or not.
        -> Create a function to check that coming fields are empty or not and if not empty then return that user and if empty then throw error.

6) Controller setup :- Create controller folder
    1) user.controller.js
        -> Now create user.controller.js to write all contolles of user in that file
        -> import our Services and models of user here then create a registerUser() function to setup the user Register functionality
        -> import the express-validator to validate our user.
        -> Create a register user function to write all register user functionality and create error function to see that any error is coming or not from that middleware which we are going to apply when we are going to call perticular rote using express validator.
        -> it's time to call all functionality's like hashPassword() generateAuthToken() of userModer and createUser() of userServices because of this we can create a user
    2) Now our hole process of user is almost finished here the last thing which is creation of Route is remaining.

7) Routing setup :- Create routes folder
    1) user.routes.js:- Create user.route.js file to create all user related routes here.
        1) /register 
            ->create roter of method post and namely '/register and give all the validation and then after validation call registerUser() controller of userController and then export router and call this perticular route in app.js use that /register route like
            Ex:- app.use('/users', {require that route here});
        
        2) /login 
            -> Create router of method post and namely /login and give all the validation to it and make loginUser() controller in userController and call that here after validation.
            -> Creation of loginUser() in userController
                => Create a loginUser() function to write all login user functionality and create error function to see that any error is coming or not from that middleware which we used in user.router.js for /login route.
                => then take all credentials from user and see that user exists in our user array of not if exists then chech their password matches of not by using comparePassword() if matches then give that user a token using generateAuthToken();
                => and send res to cookie to set this token
                => Now it's time to create Profile routes
        
        3) /profile
            ->  Create router of method get and namely /profile make getUserProfile() function in userController and call that here.
            -> Create a getUserProfile() controller in userController
                => before go to profile route we need one middleware which checks that user is having token or not there for we Create another folder namely middleware
                
                => middleware setup:- create middleware folder 
                    1) create auth.middleware.js middleware here related to authentication
                        -> import jwt, userModel and bcrypt here
                        1) authUser()
                            -> Create authUser() to see that user is having token or not
                            -> import cookie-parser and require that in app.js and use that 
                            -> first see that token exist in cookies or in header if exists then decode that using verify function of jwt and after decoded we get only that data which given while creation of token in our case we have given _id to token
                            -> now find that perticular user in our userModel by using that decoded._id using findById()
                            -> once you found that user then return to next();
                            -> finally export this middleware
                
                => Now call that authUser() middleware before calling getUserProfile() controller and then call this getUserProfle() controller

        4) /logout
        


                        



