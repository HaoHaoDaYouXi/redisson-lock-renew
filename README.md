# Redisson的锁续期


## 1.redisson的所有指令都通过lua脚本来完成，保证了原子性

## 2.redisson key的默认过期时间为30s，如果某个客户端持有一个锁超过了30s，redisson中有一个watchdog的概念，翻译过来就是![看门狗](https://user-images.githubusercontent.com/29089715/124147860-a9f6d000-dac1-11eb-8019-f541f1d32424.png)，它会在你获取锁之后，每隔10s帮你把key的超时时间设置为30s，这样的话，就算一直持有锁也不会出现key过期了其他线程获取到锁的问题了。

## 3.redisson的看门狗逻辑保证了没有死锁的发生，但是如果宕机了，看门狗也没了，此时就不会延长key的过期时间，到了时间就会自动过期，其他线程可以获取到锁。







