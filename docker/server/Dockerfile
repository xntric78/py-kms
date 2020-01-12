
FROM ubuntu

# EN: Variables\
# EN: IP-address
ENV IP		0.0.0.0
# The IP address to listen on. The default is "0.0.0.0" (all interfaces).

# EN: TCP-port
ENV PORT		1688
# The network port to listen on. The default is "1688".

# EN: ePID
ENV EPID		""
# Use this flag to manually specify an ePID to use. If no ePID is specified, a random ePID will be generated.

# EN: lcid
ENV LCID		1033
# Use this flag to manually specify an LCID for use with randomly generated ePIDs. Default is 1033 (en-us).

# EN: the current client count
ENV CLIENT_COUNT	26
# Use this flag to specify the current client count. Default is 26.
# A number >=25 is required to enable activation of client OSes; for server OSes and Office >=5.

# EN: the activation interval (in minutes)
ENV ACTIVATION_INTERVAL	120
# Use this flag to specify the activation interval (in minutes). Default is 120 minutes (2 hours).

# EN: the renewal interval (in minutes)
ENV RENEWAL_INTERVAL	10080
# Use this flag to specify the renewal interval (in minutes). Default is 10080 minutes (7 days).

# EN: Use SQLITE
ENV SQLITE		true
# Use this flag to store request information from unique clients in an SQLite database.

# EN: hwid
ENV HWID		"RANDOM"
# Use this flag to specify a HWID.
# The HWID must be an 16-character string of hex characters.
# The default is "364F463A8863D35F" or type "RANDOM" to auto generate the HWID.

# EN: log level ("CRITICAL", "ERROR", "WARNING", "INFO", "DEBUG")
ENV LOGLEVEL		DEBUG
# Use this flag to set a Loglevel. The default is "ERROR".

# EN: log file
ENV LOGFILE		/var/log/pykms_logserver.log
# Use this flag to set an output Logfile. The default is "/var/log/pykms_logserver.log".

# EN: log file size in MB
ENV LOGSIZE		""
# Use this flag to set a maximum size (in MB) to the output log file. Desactivated by default.



RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install python3-tk python3-pip
RUN pip3 install tzlocal pysqlite3 sqlite-web


RUN mkdir /opt/py-kms

# EN: Startup script
COPY start.sh /opt/py-kms/start.sh

RUN git clone https://github.com/xntric78/py-kms.git /opt/py-kms

# EN: Change permissions
RUN chmod a+x /opt/py-kms/start.sh && \

# Set Workdir
WORKDIR /opt/py-kms

# Expose ports
EXPOSE ${PORT}/tcp
EXPOSE 80/tcp
EXPOSE 8080/tcp

# Entry point
ENTRYPOINT ["/opt/py-kms/start.sh"]