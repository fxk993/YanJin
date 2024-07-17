Future、Promise和async/await的概念通常与JavaScript等异步编程环境相关联，但C++11及以后版本也引入了std::future、std::promise
# 1.std::async
接收一个可调用对象，函数对象，lambda表达式，仿函数，返回一个std::future对象
```cpp
std::future<ReturnType> future=std::async(执行策略,func,args);
\\一般这样写比较方便
auto future=std::async(std::launch::async,func,args);
```
**ReturnType**:函数返回值类型
**执行策略：**
    std::launch::async 异步执行
    std::launch::deferred 延迟执行，延迟到调用future.get()或者wait()开始
    std::launch::async|std::launch::deferred 允许选择最佳策略执行
**func**:要执行的函数
**args**：函数的参数
# 2. std::future 和 std::promise
在C++中，std::future和std::promise是用来处理异步操作的结果的。

<b style="color:green;">std::future用于获取异步操作执行的结果</b>
1.通过get方法可以获取执行的结果，如果任务未执行完成，则阻塞等待结果
2.通过wait方法可以检测是否执行完毕

<b style="color:green;">std::promise可以在异步操作中设置值或者异常</b>
1.通过set_value方法设置值或者set_exception设置异常
注意：如果异步线程设置了异常，那么future.get()的时候会重新抛出异常，一定要用try catch捕获异常，负责引发的崩溃很难排查


```cpp
#include<future>
#include<iostream>
void func() {
	std::this_thread::sleep_for(std::chrono::seconds(5));
	std::cout << "what cam i say" << std::endl;
}
int main() {
	std::future<void> future = std::async(std::launch::async, func);
	std::cout << "manba out" << std::endl;
	//future.get();如果调用的话会阻塞在这里
}
```
std::future对象通常由std::async函数或std::packaged_task::get_future()方法返回。