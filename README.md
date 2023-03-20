# gin-mall

**An e-mall based on gin+gorm+mysql read/write separation**

This project is adapted from the author [Congz](https://github.com/congz666)'s [e-mall](https://github.com/congz666/cmall-go)
Remove features such as third-party login, extreme test, third-party payment, etc., the new MySQL read-write separation, ELK logging system, and AES symmetric encryption for data desensitization.
Here also very grateful to the author of open source!

This project is more comprehensive, and more suitable for white beginners ` web development `

# Update Notes
**V2 version , the structure than the V1 version has a lot of changes **
** all transformed into the controller, dao, and service mode , more in line with enterprise development **

**V2.0 is to upload the image to the seven cows cloud **

**V2.1 is to upload images to the local static directory**

**The default main branch is v2.0, if you need v2.1, you need to pull the code of v2.1**
Such as the following command
```shell
git clone -b v2.1 git@github.com:CocaineCong/gin-mall.git
```

# Open Source Collaboration
You are welcome to pr your ideas into this project.

**Notes:**
1. You can merge branches according to your needs, remember to make sure you merge to v2.0 or v2.1 when you merge. 
2. After the CR passes, it will be merged to the v2.x branch, and the v2.0 version under the main branch will also be merged.

The previous t0 branch will be canceled and merged directly with the v2.x branch.

# Main functions of the project

- User registration and login (JWT-Go authentication)
- Modify basic user information, unbind mailbox, change password
- Posting, browsing, etc. of products
- Shopping cart addition, deletion, browsing, etc.
- Order creation, deletion, payment, etc.
- Adding, deleting, modifying addresses, etc.
- The number of views of each product, and the ranking of some types of products
- Set up payment passwords and symmetric encryption of the user's amount
- Support transactions and send back errors in the payment process
- You can upload images to object storage or switch branches to upload to the local static directory
- Add ELK system to facilitate log viewing and management

# The project needs to be improved

- Consider adding Kafka or rabbitmq, and adding a second special field

# Main dependencies of the project.
Golang V1.16
- gin
- gorm
- mysql
- redis
- ini
- jwt-go
- crypto
- logrus
- qiniu-go-sdk
- dbresolver

# Project structure
```
gin-mall/
├─ api
├─ cache
├─ conf
├─ dao
├─ doc
├─ middleware
├─ model
├─ pkg
│ ├── e
│ └── util
├─ routes
├── serializer
└── service
ðŸ™' ðŸ™'
- api : Used to define interface functions
- cache : Placement of redis cache
- conf : for storing configuration files
- dao : to operate on the persistence layer
- doc : holds the interface documentation
- middleware : application middleware
- model : Application database model
- pkg/e : encapsulates error codes
- pkg/util : utility functions
- routes : Routing logic processing
- serializer : function to serialize data to json
- service : implementation of interface functions

# configuration file
`conf/config.ini` file configuration

```ini
# debug development mode, release production mode
[service]
AppMode = debug
HttpPort = :3000

[mysql]
Db = mysql
DbHost = 127.0.0.1
DbPort = 3306
DbUser = root
DbPassWord = root
DbName = 

[redis]
RedisDb = redis
RedisAddr = 127.0.0.1:6379
RedisPw =
RedisDbName = 

[qiniu]
AccessKey = 
SerectKey = 
Bucket = 
QiniuServer = 

[email]
ValidEmail = http://localhost:8080/#/vaild/email/
SmtpHost=smtp.qq.com
SmtpEmail=
SmtpPass=
#Pass for SMTP service

[es]
EsHost = 127.0.0.1
EsPort = 9200
EsIndex = mylog
```

## Brief description
1. `mysql` is to store the main data. 2.
2. `redis` is used to store the number of product views. 3.
3. because the AES symmetric encryption algorithm is used, this algorithm is not saved in the database or file, it is the value that needs to be given when logging in for the first time, because the system will send 1w as the initial amount for shopping when logging in for the first time, so the encryption of it, the subsequent payment must be entered again, otherwise the shopping cannot be done.
4. this project uses gorm's read-write separation, so to ensure the consistency of mysql data.
5. ELK system is introduced, you can docker-compose all up, you can also run locally (make sure ES and Kibana are on)

# import interface documentation

Open postman and click import

! [postman import](doc/1. Click import to import.png)

Select the imported file
! [select import interface file](doc/2. Select file.png)

! [import](doc/3. Import.png)

Effect

! [show](doc/4.effect.png)


Here is use postman to query es, Kibana can also view es!

! [postman-es](doc/5.postman-es.png)

# Project running
**This project uses Go Mod to manage dependencies**

**Download dependencies**
```go
go mod tidy
```
**download dependencies**
```go
go run main.go

Translated with www.DeepL.com/Translator (free version)