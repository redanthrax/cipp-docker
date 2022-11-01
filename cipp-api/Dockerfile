FROM alpine:edge as build-stage
RUN apk update
RUN apk add git
WORKDIR /app
#RUN git clone https://github.com/redanthrax/CIPP-API.git .
RUN git clone -b CaseFixes https://github.com/redanthrax/CIPP-API.git .

FROM mcr.microsoft.com/azure-functions/powershell:4
ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
    AzureFunctionsJobHost__Logging__Console__IsEnabled=true \
    AzureWebJobsStorage=DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://azure-storage:10000/devstoreaccount1;QueueEndpoint=http://azure-storage:10001/devstoreaccount1;TableEndpoint=http://azure-storage:10002/devstoreaccount1;
COPY --from=build-stage /app /home/site/wwwroot
COPY ./host.json /home/site/wwwroot/host.json
