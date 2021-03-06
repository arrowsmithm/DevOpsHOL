# Avanade DevOps HOL - Lab 1 - Create a CI/CD pipeline for .NET with the Azure DevOps Project

In this lab, we setup our DevOps Project in Azure to create our CI/CD pipeline. This will provide us with a standard code base to work with.

Based on [this](https://docs.microsoft.com/en-us/vsts/build-release/apps/cd/azure/azure-devops-project-aspnetcore) tutorial.

## Prerequisites

- Complete the [Prerequisites](prerequisites.md) lab.

## Tasks

1. Go to your Azure Portal and create a new DevOps Project. Make sure it meets the following demands:
    - ASP.NET Core Web App on Windows
    - Linked to your existing VSTS account

1. When the azure resources are created, go to your VSTS account and make sure that:
   - The first Build and Release are successful
   - The App is deployed and accessable

1. Clone your code repository to your development environment and open your solution in Visual Studio:
   - Upgrade the project to ASP.NET Core 2.0 (Right-click project > Properties)
   - Update all NuGet packages to their 2.x counterparts (Right-click project > Manage NuGet packages)

1. Right-click the project and Unload it. Now edit your project file:
   - Remove the line "\<PackageTargetFallback\>$(PackageTargetFallback);portable-net45+win8+wp8+wpa81;\</PackageTargetFallback\>"

1. Add a new MSTest Test Project (.NET Core) and add a unit test class named "HomeControllerTest"
   - <details><summary>Click here to expand the sample unit test code</summary>

     ```csharp
      [TestClass]
      public class HomeControllerTest
      {
          [TestMethod]
          public void Index()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.Index() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
          }

          [TestMethod]
          public void About()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.About() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
              Assert.AreEqual("Your application description page.", result.ViewData["Message"]);
          }

          [TestMethod]
          public void Contact()
          {
              // Arrange
              HomeController controller = new HomeController();

              // Act
              ViewResult result = controller.Contact() as ViewResult;

              // Assert
              Assert.IsNotNull(result);
          }
      }
     ```
     </details>

1. Build your solution and run the unit tests. Make sure that the tests pass

1. In VSTS, edit your build definition to support .NET Core 2.0.3
   - Open task "NET Core Tool Installer" and change the version field to 2.0.3 (Do not change task version)
   ![Lab 1 netcore version](images/lab-1-netcoreversion.png)

1. Push your code to trigger a build/release

## Stretch goals

1. Add custom logging to Application Insights through your Web App

1. Export the ARM template to set up the Web App in Azure, integrate it in your Release definition

## Next steps

Continue with [Lab 2 - Add QA environment and define your multi-stage continuous deployment process with approvals and gates](lab-2-multi-stage-deployments.md).