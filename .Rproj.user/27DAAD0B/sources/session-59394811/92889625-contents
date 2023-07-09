library(tidyverse)
library(shiny)


# Define UI for application that draws a histogram
ui <- fluidPage(

    shinyFeedback::useShinyFeedback(),

    # Application title
    titlePanel("WeightR \U0001F3CB"),

    # Sidebar for settings
    sidebarLayout(
        sidebarPanel(

          numericInput("bar", "Bar weight (kg)", value = 7, min = 5, max = 200),

          radioButtons("body_part", "Body part", c("Lower body", "Upper body")),

          numericInput("previous_weight", "Last weight you lifted (kg)", value = 20, min = 10, max = 100),

          radioButtons(
            "pass", "Number of reps on your last set",
            c("> 15" = "super_pass",
              "≥ 5 and < 15" = "pass",
              "< 5" = "failed")),

          numericInput("warm", "How many warm-ups do you want?", value = 2, min = 1, max = 5),
        ),

        # Show a plot of the generated distribution
        mainPanel(
           #textOutput("new_weight"),
           htmlOutput("new_weight")
        )
    )
)

# Define server logic required to draw a histogram
server <- function(input, output) {

  new_weight <- reactive({
    # Check that bar weight is inferior or egal to previous weight
    bar_ok <- input$bar <= input$previous_weight
    shinyFeedback::feedbackWarning("previous_weight", !bar_ok, "Previous weight cannot be smaller than your bar!")
    req(bar_ok)

    if (input$pass == "super_pass") {
        if (input$body_part == "Lower body") {
          input$previous_weight + 4
        }
        else
        {
          input$previous_weight + 2
        }
    }
    else if (input$pass == "pass")
    {
      if (input$body_part == "Lower body") {
        input$previous_weight + 2
      }
      else
      {
        input$previous_weight + 1
      }
    }
    else
    {
      round(input$previous_weight - input$previous_weight * 0.1)
    }
  })

  new_weight_side <- reactive(
    (new_weight() - input$bar)/2
  )

  warm_up <- reactive({
      x <- seq(0, new_weight(), length.out = input$warm + 2) %>%
      head(-1) %>%
      tail(-1)  %>%
      round()
      x[x < input$bar] <- input$bar
      x
  })

  warm_up_side <- reactive({
    x <- (warm_up() - input$bar)/2
    x[x < 0] <- 0
    x
  })


    #output$new_weight <- renderText({
    #  paste0("Today you should lift ", new_weight(), "kg!")
    #})

    output$new_weight <- renderUI({
      str1 <- paste0("Today you should lift ", new_weight(), " kg!")
      str2 <- paste0("That is ", new_weight_side(), " kg on each side of the bar.")
      str3 <- paste0("")
      str4 <- paste0("Warm-ups should be ", str_c(warm_up(), collapse = ", "), " kg.")
      str5 <- paste0("Use ", str_c(warm_up_side(), collapse = ", "), " kg on each side of the bar.")
      HTML(paste(str1, str2, str3, str4, str5, sep = '<br/>'))

    })
}

# Run the application
shinyApp(ui = ui, server = server)
