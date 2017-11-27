# SnowFlake
每一位的具体解释

    1位，不用。二进制中最高位为1的都是负数，但是我们生成的id一般都使用整数，所以这个最高位固定是0

    41位，用来记录时间戳（毫秒）。
        41位可以表示241−1个数字，
        如果只用来表示正整数（计算机中正数包含0），可以表示的数值范围是：0 至 241−1，减1是因为可表示的数值范围是从0开始算的，而不是1。
        也就是说41位可以表示241−1个毫秒的值，转化成单位年则是(241−1)/(1000∗60∗60∗24∗365)=69年

    10位，用来记录工作机器id。
        可以部署在210=1024个节点，包括5位datacenterId和5位workerId
        5位（bit）可以表示的最大正整数是25−1=31，即可以用0、1、2、3、....31这32个数字，来表示不同的datecenterId或workerId

    12位，序列号，用来记录同毫秒内产生的不同id。
        12位（bit）可以表示的最大正整数是212−1=4096，即可以用0、1、2、3、....4095这4096个数字，来表示同一机器同一时间截（毫秒)内产生的4096个ID序号

由于在Java中64bit的整数是long类型，所以在Java中SnowFlake算法生成的id就是long来存储的。

SnowFlake可以保证：

    所有生成的id按时间趋势递增
    整个分布式系统内不会产生重复id（因为有datacenterId和workerId来做区分）
