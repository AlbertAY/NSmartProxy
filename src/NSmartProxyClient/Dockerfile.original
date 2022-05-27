
#need combile 1st.
FROM mcr.microsoft.com/dotnet/core/runtime:3.0 AS runtime
ENV PARAMS=""
WORKDIR /app
COPY / /app/
ENTRYPOINT ["dotnet", "NSmartProxyClient.dll $PARAMS"]
