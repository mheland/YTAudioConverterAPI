# YTAudioConverterAPI

## Description
YTAudioConverterAPI is a Flask-based API that allows you to convert YouTube videos into MP3 audio files. It utilizes the pytube, youtubesearchpython, yt_dlp, and pydub libraries to search for videos, extract audio, and convert it to MP3 format.

## Installation
1. Clone the repository: `git clone <https://github.com/liwa-dev/YTAudioConverterAPI.git>`
2. Navigate to the project directory: `cd YTAudioConverterAPI`
3. Install the required dependencies: `pip install -r requirements.txt`
4. Create `/mp3` directory
4. Edit `.env` file. WEBHOOK fires when audio extraction complete, API_KEY verified against `x-key` header in request

## NGINX proxy
1. Copy `nginx.conf` to `/sites-available` 
2. Update file paths and domain
3. Link `nginx.conf` to `/sites-enabled` with `sudo ln -s`
4. Restart nginx `sudo systemctl restart nginx.service`
5. Use `sudo certbot --nginx` to generate a SSL certificate
6. Reload nginx `sudo systemctl reload nginx.service`
7. Update the `.env` file with your domain in ALLOWED_ORIGINS

## Usage 
1. Start the Flask server: `python main.py`
2. Send a GET request to `/search` endpoint with the `q` parameter to search for YouTube videos.
3. Send a GET request to `/download` endpoint with the `video_url` parameter and `x-key` header to convert a YouTube video into an MP3 audio file.
4. Access the converted audio file by sending a GET request to `/mp3/<filename>` endpoint.

## API Endpoints
- `/search`: Searches for YouTube videos based on the provided query (`q` parameter).
- `/download`: Converts a YouTube video into an MP3 audio file. Requires the `video_url` parameter and `x-key` header with secret from `.env`.
- `/mp3/<filename>`: Retrieves the converted audio file.

## SYSTEMD SERVICE
Edit file paths in `yt-rip.service` and install as systemd service with 

`sudo cp yt-rip.service /etc/systemd/system/yt-rip.service && sudo systemctl daemon-reload && sudo systemctl restart yt-rip.service && sudo systemctl status yt-rip.service`

## COOKIES
Log in to YouTube and save youtube.com cookies using Firefox plugin. Store in cookies.txt in the same directory as main.py
https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/

You can also have local `yt-dlp` generate the cookie file with 

`yt-dlp --cookies-from-browser BROWSER --cookies cookies.txt https://www.youtube.com`

For BROWSER use chrome, chromium, firefox, opera, edge, or safari

## .env file
Replace example.com with live domain
```
API_KEY=mysecret12345
WEBHOOK_URL=https://www.example.com/123
ALLOWED_ORIGINS=http://localhost,http://localhost:3000,https://example.com
RETENTION_PERIOD=7200
BASE_URL=https://example.com
```

## Contributing
Contributions are welcome! If you have any suggestions, bug reports, or feature requests, please open an issue or submit a pull request.

## License
This project is licensed under the [MIT License](LICENSE).
