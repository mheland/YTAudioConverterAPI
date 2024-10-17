# YTAudioConverterAPI

## Description
YTAudioConverterAPI is a Flask-based API that allows you to convert YouTube videos into MP3 audio files. It utilizes the pytube, youtubesearchpython, yt_dlp, and pydub libraries to search for videos, extract audio, and convert it to MP3 format.

## Installation
1. Clone the repository: `git clone <https://github.com/liwa-dev/YTAudioConverterAPI.git>`
2. Navigate to the project directory: `cd YTAudioConverterAPI`
3. Install the required dependencies: `pip install -r requirements.txt`

## NGINX
1. Save `nginx.conf` to `/sites-available` and edit file paths and domain
2. Link `nginx.conf` to `/sites-enabled` with `sudo ln -s`
3. Use `sudo certbot --nginx` to generate a SSL certificate
4. Edit the `.env` file with your domain in ALLOWED_ORIGINS


## Usage
1. Start the Flask server: `python main.py`
2. Send a GET request to `/search` endpoint with the `q` parameter to search for YouTube videos.
3. Send a GET request to `/download` endpoint with the `video_url` parameter to convert a YouTube video into an MP3 audio file.
4. Access the converted audio file by sending a GET request to `/mp3/<filename>` endpoint.

## API Endpoints
- `/search`: Searches for YouTube videos based on the provided query (`q` parameter).
- `/download`: Converts a YouTube video into an MP3 audio file. Requires the `video_url` parameter and `x-key` definced in .env.
- `/mp3/<filename>`: Retrieves the converted audio file.

## SYSTEMD SERVICE
Edit file paths in `yt-rip.service` and install as systemd service with 
`sudo cp yt-rip.service /etc/systemd/system/yt-rip.service && sudo systemctl daemon-reload && sudo systemctl restart yt-rip.service && sudo systemctl status yt-rip.service`

## Contributing
Contributions are welcome! If you have any suggestions, bug reports, or feature requests, please open an issue or submit a pull request.

## License
This project is licensed under the [MIT License](LICENSE).
