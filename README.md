# lab4

+ Workflow – это высокоуровневый набор правил для того, чтобы делать какие-то действия при определенных условиях.

+ Job – это сущность, которая запускает какую-то задачу в рамках вашего workflow.

+ Step – это шаг. Т. е. один job может состоять из нескольких шагов.

+ Action – это тот переиспользуемый unit, который попал в название GitHub Actions, т. е. это самая минимальная часть, которую можно переиспользовать в нашем CI.

+ Event – это термин, который обозначает, что случилось какое-то действие. А если действие случилось, то мы запускаем какой-то конкретный workflow.


+ Checkout – это всегда первый action, т. е. это тот action, который копирует ваш код и делает git pull в текущую папку.


Включение автоматизации происходит добавлением файлов YAML\
в специальную директорию .github/workflows в вашем Repository 
```
.github/workflows/testing.yml

*.yml - имя файла YAML может быть любым
```

My *.yml\
```
name: CI # Непрерывная интеграция (CI): автоматическая сборка и тестирование 
on:
  push: # запустить при push на ветку main 
    branches: [ main ]
jobs:
  build_all_libraries:
    runs-on: ubuntu-latest # какие образы используются
    steps:
      
      - uses: actions/checkout@v3

      - name: prepairing # Название задачи
        run: sudo apt install cmake g++ clang-11 # Задача
      
      - name: Building of forrmater_lib 
        run: |
         cd formatter_lib
         cmake . -DCMAKE_CXX_COMPILER=clang++
         cmake --build .
         cd ..
        
      - name: Building of forrmater_ex_lib
        run: |
          cd formatter_ex_lib
          cmake . -DCMAKE_CXX_COMPILER=clang++
          cmake --build .
          cd ..
          
      - name: Building of hello_world_application
        run: |
          cd hello_world_application
          cmake . -DCMAKE_CXX_COMPILER=clang++
          cmake --build .
          cd ..
          
      - name: Building of solver_lib
        run: |
          cd solver_lib
          cmake . -DCMAKE_CXX_COMPILER=clang++
          cmake --build .
          cd ..
          
      - name: Building of solver_application
        run: |
          cd solver_application
          cmake . -DCMAKE_CXX_COMPILER=clang++
          cmake --build .
          cd .. 
```
