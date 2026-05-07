# Deployment notes

## To shinyapps.io (current production)

```r
# one-time auth
install.packages("rsconnect")
rsconnect::setAccountInfo(name   = "emmacorley",
                          token  = "<your-token>",
                          secret = "<your-secret>")

# deploy
rsconnect::deployApp(
  appDir   = ".",
  appName  = "irt_app",
  appTitle = "HARMOODS — Harmonised Depression Score Converter"
)
```

Tokens are at https://www.shinyapps.io/admin/#/tokens. The free tier is sufficient for this app.

## To Posit Connect / Cloud

`rsconnect::deployApp()` works the same way — just choose the matching server.

## To a local Docker container

A minimal Dockerfile:

```dockerfile
FROM rocker/shiny:4.3.2
RUN R -e "install.packages(c('bslib','readr','readxl','writexl','dplyr','tidyr','tibble','purrr','stringr','ggplot2'))"
COPY . /srv/shiny-server/harmoods/
EXPOSE 3838
```

Build and run:
```bash
docker build -t harmoods .
docker run -p 3838:3838 harmoods
# visit http://localhost:3838/harmoods
```

## To GitHub Pages?

**Not possible** — Shiny apps need a running R server, which GitHub Pages does not provide. The source code lives on GitHub; the live app lives on shinyapps.io, Posit Connect, or your own R server.
