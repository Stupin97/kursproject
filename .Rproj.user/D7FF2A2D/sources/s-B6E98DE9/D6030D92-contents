#install.packages("shiny")
#install.packages("Rssa")

library(shiny)

#Пользовательский интерфейс
shinyUI(fluidPage(
  #Заголовок
  titlePanel(h4('Демонстрация возможностей языка R с помощью пакета SHINY', align="center")),
  sidebarLayout(
    #Сайд бар
    sidebarPanel(
      #Виджет для выпадающего списка
      selectInput("dataset", "Выберите данные", choices = c("Данные с метеостанции за 01.11.2018",
                                                            "Данные с метеостанции за 01.01.2019",
                                                            "Данные с метеостанции за 15.01.2019")),
      br(),
      
      numericInput("obs", "Выбрать первых N строк", 10),
      
      submitButton("Обновить"),
      
      br(),
      
      #Лэйбол для информативной подсказки 
      helpText("Выберите формат данных для скачивания"),
      
      #Панель однозначного выбора
      radioButtons("type", "Форматы данных:",
                   choices = c("Excel (CSV)", "Text (TSV)", "Text (С пробелами)", "Docx")),
      
      br(),
      
      #Лэйбол для информативной подсказки 
      helpText("Нажмите для скачивания"),
      
      #Кнопка скачивания
      downloadButton('downloadData', 'Download')
    ),
    #Основная панель
    mainPanel(
      #Таблицы
      tableOutput('table'),
      tableOutput("view")
    )
  )
))