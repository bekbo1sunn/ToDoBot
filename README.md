# TODO bot

>Это базовый телеграм бот на классах

## Возможности бота 

> Добавлеие задач

```
    def handle_add(self, message):
        self.bot.reply_to(message, "Введите новую задачу:")
        self.bot.register_next_step_handler(message, self.add_task)

    def add_task(self, message):
        task = message.text
        self.tasks.append(task)
        self.bot.reply_to(message, "Задача успешно добавлена!")
```
> Просмотр задач

```
    def handle_tasks(self, message):
        task_list = ""
        if self.tasks:
            for index, task in enumerate(self.tasks):
                task_list += f"{index + 1}. {task}\n"
        else:
            task_list = "Список задач пуст."
        self.bot.reply_to(message, task_list)
```
> Изменение задач
```
    def update_task(self, message):
        task_index = int(message.text) - 1
        if 0 <= task_index < len(self.tasks):
            self.bot.reply_to(message, f"Введите новое значение для задачи \"{self.tasks[task_index]}\":")
            self.bot.register_next_step_handler(message, self.save_updated_task, task_index)
        else:
            self.bot.reply_to(message, "Неверный номер задачи.")

    def save_updated_task(self, message, task_index):
        new_task = message.text
        self.tasks[task_index] = new_task
        self.bot.reply_to(message, "Задача успешно обновлена!")
```
> Удаляние задач

```
    def handle_delete(self, message):
        self.bot.reply_to(message, "Введите номер задачи, которую хотите удалить:")
        self.bot.register_next_step_handler(message, self.delete_task)

    def delete_task(self, message):
        task_index = int(message.text) - 1
        if 0 <= task_index < len(self.tasks):
            deleted_task = self.tasks.pop(task_index)
            self.bot.reply_to(message, f"Задача \"{deleted_task}\" успешно удалена!")
        else:
            self.bot.reply_to(message, "Неверный номер задачи.")
```


>***Чуть позже возможно ещё новые функции добавлю, но пока что это всё***
