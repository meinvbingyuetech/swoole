## 定时任务
   - 如果感觉没运行起来，则修改一下函数名后试试，可以尝试使用版本号V1、V2
   
   - 修改后，记得重启牛
   
   - 记得要安装pcre-dev
   ```
   sudo apt-get update 
   sudo apt-get install libpcre3 libpcre3-dev 
   ```
   
   - 内存溢出，尝试修改下面的代码
      - vendor\swoft\task\src\Crontab\TableCrontab.php
   ```
      const TABLE_SIZE = 1024;
   ```

   - 清理任务
      - vendor\swoft\task\src\Crontab\Crontab.php
   ```php
   /**
     * 清理执行任务表
     */
    private function cleanRunTimeTable()
    {
        foreach ($this->getRunTimeTable()->table as $key => $value) {
            if ($value['runStatus'] === self::FINISH || $value['sec'] < time()) {
                $this->getRunTimeTable()->del($key);
            }
        }
    }

    /**
     * 获取执行任务表数据
     */
    public function getRunTimeTableData()
    {
        $arr = [];
        foreach ($this->getRunTimeTable()->table as $key => $value) {
            $arr[] = $value;
        }
        return $value;
    }
   ```
   
   ```php
   /* @var \Swoft\Task\Crontab\Crontab $cron*/
   $cron = App::getBean('crontab');

   $arr = $cron->getRunTimeTableData();
   ConsoleUtil::log("-------------------------------------------",[$arr]);

   $arr = $cron->getTasks();
   ConsoleUtil::log("-------------------------------------------",[$arr]);
   ```
