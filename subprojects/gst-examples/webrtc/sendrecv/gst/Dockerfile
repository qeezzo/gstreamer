# Use the official Python base image
FROM python:bookworm

# Install necessary system dependencies for gstreamer and websockets
RUN apt-get update && apt-get install -y \
    gstreamer1.0-tools \
    gstreamer1.0-plugins-base \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-bad \
    gstreamer1.0-libav \
    gstreamer1.0-alsa \
    gstreamer1.0-gl \
    gstreamer1.0-rtsp \
    gstreamer1.0-plugins-ugly \
    libgstreamer1.0-dev \
    libgstreamer-plugins-base1.0-dev \
    libgstreamer-plugins-bad1.0-dev \
    libglib2.0-dev \
    libsoup2.4-dev \
    libnice-dev \
    meson \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update
RUN apt-get install -y \
  libcairo2-dev \
  gobject-introspection \
  libgirepository1.0-dev \
  girepository-2.0 \
  python3-gst-1.0 \
  python3-gi \
  gstreamer1.0-python3-plugin-loader \
  gir1.2-gstreamer-1.0

RUN apt-get install -y \
    libnice-dev \
    gstreamer1.0-nice

# Install required Python dependencies
RUN pip install --no-cache-dir \
  websockets==15.0.0 \
  PyGObject==3.50.0

# Set the working directory
WORKDIR /app

# Copy the Python script to the container
COPY . /app/

# Expose the port used by the app (adjust if necessary)
EXPOSE 8443

# Set the entrypoint to run the Python script
# ENTRYPOINT ["python3", "webrtc_sendrecv.py", "--peer-id=1", "--server=ws://signalling:8443"]

CMD echo "Waiting a few seconds for you to open the browser at localhost:8080" \
    && sleep 10 \
    && GST_DEBUG=3 ./webrtc_sendrecv.py \
    --peer-id=1 \
    --server=ws://signalling:8443

