### 基礎 aws 設置
#### RDS
1. name: world press
2. security group: 設定為 ec2 的 security group，type 改為 MYSQL/Aurora
讓 ec2 可以存取 ec2

#### EC2
1. amazone machine engine : Amazon Linux 2 AMI (HVM), SSD Volume Type
2. instance type : t2 micro
3. ssh 登入並建置 mysql DB 
`sudo yum install -y mysql` 安裝 mysql
`export MYSQL_HOST=worldpress.chauctukxvgo.us-east-2.rds.amazonaws.com` 建立 MUSQL_HOST env
`mysql --user=<user> --password=<password>` 連線DB
建立 wordpress 使用者並賦予權限
`CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
FLUSH PRIVILEGES;
Exit`
4. 安裝 apache `sudo yum install -y httpd`
5. 測試頁 `sudo service httpd start`

#### EC2 部屬 world press
`ssh -i ~/desktop/hittheroad.pem ec2-user@3.16.108.105`
``` js
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
``` 
下載並解壓縮 wp
``` js
cd wordpress
cp wp-config-sample.php wp-config.php
``` 
進入並建立 php 組態檔
`nano wp-config.php` 編輯組態檔
```js
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** MySQL database username */
define( 'DB_USER', 'username_here' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password_here' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );
```

```js
/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define( 'AUTH_KEY',         'put your unique phrase here' );
define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
define( 'NONCE_KEY',        'put your unique phrase here' );
define( 'AUTH_SALT',        'put your unique phrase here' );
define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
define( 'NONCE_SALT',       'put your unique phrase here' );
```
`ctrl + O` nano 儲存
`ctrl + X` nano 退出

### 下載主題
`sudo chown -R apache:apache path/to/wordpress`
因為 ec2 預設不給 apache sudo 權限，所以會出現需要用 ftp 連線的要求，這時候需要透過上面指令更改權限

### 登入 path
ㄧ般畫面: ip / domain
登入位置: path/wp-admin/

![](Pasted%20image%2020210704005957.png)


### reference
(aws 官方教學)[https://aws.amazon.com/tw/getting-started/hands-on/deploy-wordpress-with-amazon-rds/]


