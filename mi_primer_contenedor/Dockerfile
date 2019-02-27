#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1803 AS base
WORKDIR /app
EXPOSE 65519
EXPOSE 44323

FROM microsoft/dotnet:2.1-sdk-nanoserver-1803 AS build
WORKDIR /src
COPY ["mi_primer_contenedor/mi_primer_contenedor.csproj", "mi_primer_contenedor/"]
RUN dotnet restore "mi_primer_contenedor/mi_primer_contenedor.csproj"
COPY . .
WORKDIR "/src/mi_primer_contenedor"
RUN dotnet build "mi_primer_contenedor.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "mi_primer_contenedor.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "mi_primer_contenedor.dll"]