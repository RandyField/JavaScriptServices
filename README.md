# JavaScriptServices [Archived]

## IMPORTANT

The features described in this article are obsolete as of ASP.NET Core 3.0. A simpler SPA frameworks integration mechanism is available in the [Microsoft.AspNetCore.SpaServices.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices.Extensions) NuGet package. For more information, see [[Announcement] Obsoleting Microsoft.AspNetCore.SpaServices and Microsoft.AspNetCore.NodeServices](https://github.com/dotnet/AspNetCore/issues/12890).


## What is this?

`JavaScriptServices` is a set of client-side technologies for ASP.NET Core. It provides infrastructure that you'll find useful if you:

-  Use Angular / React / Vue / Aurelia / Knockout / etc.
-  Build your client-side resources using Webpack.
-  Execute JavaScript on the server at runtime.

Read [Building Single Page Applications on ASP.NET Core with JavaScriptServices](https://blogs.msdn.microsoft.com/webdev/2017/02/14/building-single-page-applications-on-asp-net-core-with-javascriptservices/) for more details.

This repo contains:

 * A set of NuGet/NPM packages that implement functionality for:
   * Invoking arbitrary NPM packages at runtime from .NET code ([docs](/src/Microsoft.AspNetCore.NodeServices#simple-usage-example))
   * Server-side prerendering of SPA components ([docs](/src/Microsoft.AspNetCore.SpaServices#server-side-prerendering))
   * Webpack dev middleware ([docs](/src/Microsoft.AspNetCore.SpaServices#webpack-dev-middleware))
   * Hot module replacement (HMR) ([docs](/src/Microsoft.AspNetCore.SpaServices#webpack-hot-module-replacement))
   * Server-side and client-side routing integration ([docs](/src/Microsoft.AspNetCore.SpaServices#routing-helper-mapspafallbackroute))
   * Server-side and client-side validation integration
   * "Lazy loading" for Knockout apps
 * Samples and docs

It's cross-platform (Windows, Linux, or macOS) and works with .NET Core 2.0 or later.

## Creating new applications

Prerequisites:

* [.NET Core 2.0](https://www.microsoft.com/net/core) (or later) SDK
* [Node.js](https://nodejs.org/) version 6 (or later)

With these prerequisites, you can immediately create new ASP.NET Core applications that use Angular, React, or React+Redux without having to install anything extra.

### Option 1: Creating Angular/React/Redux applications from the command line (cross-platform)

In an empty directory, run (for example) `dotnet new angular`. Other supported SPA frameworks include React and React+Redux. You can see the list of available SPA templates by running `dotnet new spa`.

Once the generator has run and restored all the dependencies, you can start up your new ASP.NET Core SPA:

    npm install
    dotnet run

### Option 2: Creating Angular/React/Redux applications using Visual Studio 2017 Update 3 or later (Windows only)

Using the `File`->`New Project` dialog, select *ASP.NET Core Web Application*. You will then be offered the option to create an application with Angular, React, or React+Redux. When the application is created, you can build and run it in the normal way.

### More info and other SPA frameworks

For a more detailed (albeit somewhat outdated) walkthrough, see [getting started with the `aspnetcore-spa` generator](http://blog.stevensanderson.com/2016/05/02/angular2-react-knockout-apps-on-aspnet-core/).

If you want to build an ASP.NET Core application with Aurelia, Knockout, or Vue, you can use the `Microsoft.AspNetCore.SpaTemplates` package. On the command line, run `dotnet new --install Microsoft.AspNetCore.SpaTemplates`. Then you will be able to run `dotnet new aurelia` (or `dotnet new vue`, etc.) to create your new application.

## Adding to existing applications

If you have an existing ASP.NET Core application, or if you just want to use the underlying JavaScriptServices packages directly, you can install these packages using NuGet and NPM:

 * `Microsoft.AspNetCore.NodeServices`
   * This provides a fast and robust way for .NET code to run JavaScript on the server inside a Node.js environment. You can use this to consume arbitrary functionality from NPM packages at runtime in your ASP.NET Core app.
   * Most applications developers don't need to use this directly, but you can do so if you want to implement your own functionality that involves calling Node.js code from .NET at runtime.
   * Find [documentation and usage examples here](/src/Microsoft.AspNetCore.NodeServices#microsoftaspnetcorenodeservices).
 * `Microsoft.AspNetCore.SpaServices`
   * This provides infrastructure that's generally useful when building Single Page Applications (SPAs) with technologies such as Angular or React (for example, server-side prerendering and webpack middleware). Internally, it uses the `NodeServices` package to implement its features.
   * Find [documentation and usage examples here](/src/Microsoft.AspNetCore.SpaServices#microsoftaspnetcorespaservices)

There were previously other packages called  `Microsoft.AspNetCore.AngularServices` and `Microsoft.AspNetCore.ReactServices` but these are not currently needed - all applicable functionality is in `Microsoft.AspNetCore.SpaServices`, because it's sufficiently general.

If you want to build a helper library for some other SPA framework, you can do so by taking a dependency on `Microsoft.AspNetCore.SpaServices` and wrapping its functionality in whatever way is most useful for your SPA framework.

## Samples

The [`samples` directory](/samples) contains examples of:

- Using the JavaScript services family of packages with Angular and React.
- A standalone `NodeServices` usage for runtime code transpilation and image processing.

**To run the samples:**

 * Clone this repo
 * At the repo's root directory (the one containing `src`, `samples`, etc.), run `dotnet restore`
 * Change directory to the sample you want to run (for example, `cd samples/angular/MusicStore`)
 * Restore Node dependencies by running `npm install`
   * If you're trying to run the Angular "Music Store" sample, then also run `gulp` (which you need to have installed globally). None of the other samples require this.
 * Run the application (`dotnet run`)
 * Browse to [http://localhost:5000](http://localhost:5000)
