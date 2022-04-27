FROM java:openjdk-8-jdk


RUN rm -rf Mule
RUN mkdir Mule

#Add  Mule runtime from our local system to the Docker container
CMD echo "--- Adding Mule4.4.0 runtime in Docker Container ---"
ADD  mule-ee-distribution-standalone-4.4.0.zip /Mule

#Adding Work Directory
CMD echo "--- Adding Work Directory ---"
WORKDIR /Mule

#Extract and install the Mule runtime in the container
CMD echo "--- Unzipping the added zip ---"
RUN         unzip mule-ee-distribution-standalone-4.4.0.zip && \
            rm mule-ee-distribution-standalone-4.4.0.zip
			
# Define volume mount points
VOLUME      ["/Mule/mule-enterprise-standalone-4.4.0/logs", "/Mule/mule-enterprise-standalone-4.4.0/apps", "/Mule/mule-enterprise-standalone-4.4.0/domains"]

# Copy and install license
#CMD echo "--- Copy and install license ---"
#COPY        license.lic mule-enterprise-standalone-4.4.0/conf/
#RUN         mule-enterprise-standalone-4.4.0/bin/mule -installLicense mule-enterprise-standalone-4.4.0/conf/license.lic

#Check if Mule Licence installed
RUN ls -ltr mule-enterprise-standalone-4.4.0/conf/
CMD echo "------ Licence installed ! --------"

#Copy and deploy mule application in runtime
CMD echo "--- Deploying mule application in runtime ---"
COPY  callingExternalAPI.jar mule-enterprise-standalone-4.4.0/apps/
RUN ls -ltr mule-enterprise-standalone-4.4.0/apps/

# Expose the necessary port ranges as required by the Mule Apps
EXPOSE      8081-8085
EXPOSE      9000
EXPOSE      9082

# Mule remote debugger
EXPOSE      5000

# Mule JMX port (must match Mule config file)
EXPOSE      1098

# Mule MMC agent port
EXPOSE      7777

# AMC agent port
EXPOSE      9997

# Start Mule runtime
CMD echo "--- Starting Mule runtime ---"
CMD         ["mule-enterprise-standalone-4.4.0/bin/mule"]