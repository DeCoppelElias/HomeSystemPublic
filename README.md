# Home System
I developed a home automation system, which is powered by a Python server using the Flask framework. This server is designed to manage various functions within the house and allows authenticated users on the local network to control these features remotely. By leveraging Flask's capabilities, the server handles incoming requests from users, verifies their authentication, and then performs the requested actions. This setup provides a secure and efficient way for household members to interact with and automate different aspects of their home environment.

# What I learned
Through developing this home automation system, I learned about many security measures, including encryption, 2-factor authentication, and rate limiting, which are essential for protecting user data and ensuring only authorized access. I also learned the importance of CSRF protection and password hashing to defend against common web vulnerabilities. Additionally, I implemented logging and alerting mechanisms for monitoring and responding to critical actions, as well as using pre-commit hooks to maintain code quality and consistency. These features collectively contribute to a secure, reliable, and maintainable system.

# Security
A home system should only be accessible by authenticated users and only authenticated users should be able to perform actions. This makes security one of the top priorities of this type of system.
## General Security Flow
First the user needs to obtain a confirmation code by entering their email and password. This request will send the confirmation code to the email if that user exists and the password is correct. Then, the user will need to log in with their email, password and confirmation code.
## Security Features
### - Encryption
Communication is encrypted using TLS. The server is contacted using the HTTPS protocol.
### - 2 factor authentication
2 factor authentication is achieved by requiring an email-password combination and a confirmation code. This confirmation code is sent to the email of the user.
### - Rate Limiting
The back-end has rate limiting to protect the server from request spamming. There are general rate limits (200 per day, 50 per hour), and also specific rate limits for specific endpoints.
### - CSRF Protection
A CSRF token is used for every POST request, this mean that a POST requests can only be performed after first sending a GET request.
### - Password hashing
All passwords are hashed and stored in a database. When a password is checked, the hash of that password is compared with the password in the database.
### - Alerting
Special actions will send an alert to the master user via email. This email will contain information about which critical action was performed, when it was performed and by who.

# Other
### - Pre-commit
Pre-commit was used to to simple checks before being able to commit. These checks include import sorting and line length checking.
### - Logging
All requests to the server are logged in a log file together with additional information and warnings. A new log file is created daily and log files that are older than 1 month are automatically deleted.

# Used Flask Extensions
- flask_bcrypt: hashing passwords
- flask_cors: CORS protection
- flask_login: user authentication
- flask_mail: sending emails
- flask_sqlalchemy: creating a database and storing user information
- flask_wtf.csrf: CSRF protection
