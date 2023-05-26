<style>
  @import url('https://fonts.googleapis.com/css2?family=Dosis&display=swap');
</style>
<html>
<head>
  <title>Top Songs</title>
</head>
<body>
  <h1>Top Songs</h1>
  <ul id="playlistTracks"></ul>

  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <link rel="stylesheet" href="./index.min.css" />
  <script>
    // Set up Spotify credentials and endpoints
    const client_id = '5b33a3c946234840adf56c4e858a7032';
    const client_secret = 'fc9a87ca2d05461e9fd5041ab44e5be1';
    const authEndpoint = 'https://accounts.spotify.com/api/token';

    // Get access token using client credentials flow
    async function getAccessToken() {
      const response = await axios.post(authEndpoint, null, {
        params: {
          grant_type: 'client_credentials',
          client_id: client_id,
          client_secret: client_secret
        }
      });

      return response.data.access_token;
    }

    // Get playlist tracks using Spotify Web API
    async function getPlaylistTracks(playlistId, accessToken) {
      const playlistTracksEndpoint = `https://api.spotify.com/v1/playlists/${playlistId}/tracks`;

      const response = await axios.get(playlistTracksEndpoint, {
        headers: {
          Authorization: `Bearer ${accessToken}`
        }
      });

      return response.data.items;
    }

    // Update the HTML with the retrieved track information
    async function displayPlaylistTracks() {
      const playlistLink = 'https://open.spotify.com/playlist/37i9dQZEVXbNG2KDcFcKOF?si=1333723a6eff4b7f';
      const playlistId = playlistLink.split('/').pop().split('?')[0];

      const accessToken = await getAccessToken();
      const playlistTracks = await getPlaylistTracks(playlistId, accessToken);

      const playlistTracksElement = document.getElementById('playlistTracks');
      playlistTracks.forEach(track => {
        const trackName = track.track.name;
        const li = document.createElement('li');
        li.textContent = trackName;
        playlistTracksElement.appendChild(li);

        // Additional track information retrieval
        // const artistName = track.track.artists[0].name;
        // const artistLi = document.createElement('li');
        // artistLi.textContent = artistName;
        // playlistTracksElement.appendChild(artistLi);
      });
    }

    displayPlaylistTracks();
  </script>
</body>
</html>