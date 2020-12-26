library(shiny)
library(datasets)
library("Rssa")

#Серверная функция (скелет)
shinyServer(
  function(input, output){
    #Заполнение выпадающего списка
    firstDate <- read.csv(file="./date01.11.2018.csv", header = TRUE)
    secondDate <-read.csv(file="./date01.01.2019.csv", header = TRUE)
    thridDate <-read.csv(file="./date15.01.2019.csv", header = TRUE)
    
    datasetInput <- reactive({
      switch (input$dataset,
              "Данные с метеостанции за 01.11.2018" = firstDate,
              "Данные с метеостанции за 01.01.2019" = secondDate,
              "Данные с метеостанции за 15.01.2019" = thridDate
      )
    })
    
    #Реактивная функция для выбора формата скаченного файла
    fileext <- reactive({
      switch (input$type,
        "Excel (CSV)" = "csv",
        "Text (TSV)" = "txt",
        "Text (С пробелами)" = "txt",
        "Docx" = "docx"
      )
    })
    
    #Отображение таблицы
    #output$table <- renderTable({
    #  datasetInput()
    #})
    
    #Отображение таблицы (количесвтом строк определенным пользователем)
    output$view <- renderTable({
      head(datasetInput(), n = input$obs)
    })
    
    #downloadHandler - два аргумента
    output$downloadData <- downloadHandler(
      #Имя файла
      filename = function(){
        paste(input$dataset, fileext(), sep = ".")
      },
      
      #Ланные для файла
      content = function(file){
        sep <- switch (input$type,
                       "Excel (CSV)" = ",",
                       "Text (TSV)" = "\t",
                       "Text (С пробелами)" = " ",
                       "Docx" = " "
        )
        
        #Производим запись в указанный файл
        write.table(datasetInput(), file, sep = sep,
                    row.names = FALSE)
      }
    )
  }
)