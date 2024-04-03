# safe-down-casting
Consider Safe and Simple Down Casting using static_cast

```cpp
#include <iostream>

class Task
{
    public:
    void show()
    {
        std::cout << "Task" << std::endl;
    }


};

class MyTask : public Task
{
    public:
    void show()
    {
        std::cout << "MyTask" << std::endl;
    }
};

template<typename T>
class TaskCastHelper
{
    private:
    Task* task_;

    public:
    TaskCastHelper(T* task)
    : task_(static_cast<Task*>(task))
    {

    }

    Task* get()
    {
        return task_;
    }

    T* get_safe_cast()
    {
        return static_cast<T*>(task_);
    }
};

int main()
{
    MyTask task;

    TaskCastHelper<MyTask> helper(&task);

    helper.get()->show();
    helper.get_safe_cast()->show();

    return 0;
}
```
