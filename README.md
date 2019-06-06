# shell、Linux、laravel常用命令

    cd 到相应目录
    grep命令用于查找文件里符合条件的字符串。
    sudo -Hu www 用www要执行

### less [参数] 文件 
    less laravel-2019-04-19.log
### tail [参数] [文件]  
    -f 循环读取 
    tail -f * 当前目录 循环读取 
    tail -f laravel-2019-04-19.log |grep 'test' 

### cat 命令用于连接文件并打印到标准输出设备上。
    cat laravel-2019-04-19.log  |grep 'test'

### 权限chmod
    chmod +x ./* 这个目录具有执行权限
    chmod +x ./test.sh  #使这个脚本具有执行权限

### gzip解压
    gzip -d laravel-2019-04-19.log.gz 

### ps
    ps -e -f 查看所有的进程

    kill掉进程名包含test的进程 ：ps -ef | grep 'test' | grep -v grep | cut -c 9-15 | xargs kill -s 9 



### pm2管理

    新加时 sudo -Hu www ./pm2_Start.sh 
    
    整个重启重启  wwwpm2 restart all
    
    重启单个进程  wwwpm2 restart xxxx
    
    临时关闭wwwpm2 stop xxxx
    
    长期的wwwpm2 delete xxxx
    
    临时关闭关键词wwwpm2 stop \xxxx\  





### crontab

    查看 crontab -e -u www
    
    08 11 * * * php /home/zengyanyu/zengyanyu.onedollars.dev.zhimafx.xyz/artisan test  ##11点08分执行 php artisan  test
    
    sudo -Hu www php artisan test //手动执行



### 创建异步 
    php artisan make:job TestJob --queued
    php artisan  queue:work --queue=test --daemon --tries=3 --sleep=0    手动执行

### 数据库 —— 迁移
    创建php artisan make:migration create_users_table --create=users
    
     Schema::create('test', function (Blueprint $table) {
            $table->engine = 'InnoDB';
            $table->increments('id');
            $table->string('title')->default(0)->comment('标题');
            $table->tinyinteger('status')->default(0)->comment('状态 1显示 2不显示');
            $table->integer('c_time')->default(0);
            $table->integer('u_time')->default(0);
            $table->index('status');
        });
        \DB::statement("ALTER TABLE `test` comment '测试'");

    执行 php artisan migrate

