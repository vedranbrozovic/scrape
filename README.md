# scrape
#IKEA get prices
#using rvest see: https://blog.rstudio.com/2014/11/24/rvest-easy-web-scraping-with-r/
#vedran brozovic

install.packages("rvest")
library(rvest)    #for scraping
library(stringr)  #it's just easier to manipulate strings


articleNO<-"00374297"
country<- "de/de"

#setting up the URL of a webpage
strHTML<-str_c("https://www.ikea.com/", country, "/catalog/products/",articleNO,
               sep = "", 
               collapse = NULL)

#strHTML<-paste("https://www.ikea.com/de/de/catalog/products/",articleNO)

ikea_article <- read_html(strHTML)

price1<-ikea_article %>%
  html_node("#price1") %>%
  html_text()

#getting the price in local currency from messy string
  price<-toString(price1)
  price<-str_replace_all(price,"\t","")
  price<-str_replace_all(price,"\r","")
  price<-str_replace_all(price,"\n","")
  price<-str_replace_all(price,"kn","")
  (price<-str_trim(price))
  (priceNo<-as.numeric(price))

