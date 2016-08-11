## StudyForRAC

study for https://github.com/shuaiwang007/RAC

If you have some questions, please tell me.

### RAC是一个非常强大的框架我们将会从以下方面去介绍它

* RACSignal
* RACSubject
* RACSequence
* RACMulticastConnection
* RACCommand

### RAC框架如何pod导入项目

- 首先在podfile里把use_frameworks!的注释取消掉,即把#删掉即可

- 再然后可以添加上 pod 'ReactiveCocoa', '~> 4.1.0'

- pod install即可

- 使用时只要将 'ReactiveCocoa.h' 'NSObject+RACKVOWrapper.h' 'RACReturnSignal.h' 这三个文件导入就可以了

- 注意:若出现大量报错的话,请将Xcode升级至7.3以上

#### RACSignal

- 我们首先要创建一个信号

        RACSignal * signal = [RACSignal createSignal:^RACDisposable *(id<RACSubscriber> subscriber) {

            [subscriber sendNext:@"信号内容/signal content"];
            //这里采用的是链式编程
            return [RACDisposable disposableWithBlock:^{

            NSLog(@"此时取消订阅");

            }];

        }];
        
- 下来我们要订阅这个信号
        RACDisposable * disposable = [self.signal subscribeNext:^(id x) {

        NSLog(@"%@",x);

        }];

- 最后不要忘记取消订阅

        [disposable dispose];

和通知很像,有通知的发出者和接收者,最后也一样要取消订阅,值得一提的是,使用RAC发送通知最后不用取消通知

- 未完待续