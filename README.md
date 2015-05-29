# PowershellHttpHandler
IIS Http Handler to execute Powershell files

# Installation
Place PowershellHttpHandler.dll in the \bin folder of your ISS site

Edit `web.config` with

  <configuration>
      <system.webServer>
          <handlers>
              <add name="Powershell" path="*.ps1" verb="*" type="System.Web.Handlers.PowershellHandler" preCondition="integratedMode" />
          </handlers>
          <defaultDocument>
              <files>
                  <add value="index.ps1" />
              </files>
          </defaultDocument>
      </system.webServer>
  </configuration>

# Usage
Example `index.ps1`

  @"
  <html>
    <head>
      <title>Powershell Handler Test</title>
    </head>
    <body>
      <p>Hello, $(Get-Variable $HttpContext.Request.LogonUserIdentity)!</p>
    </body>
  </html>
  "@
  
The variable `$HttpContext` is passed on every page and contains the server `HttpContext` object.

# Config
If you want to configure your webapp you could place a file named `config.ps1` that will be executed on session start.
