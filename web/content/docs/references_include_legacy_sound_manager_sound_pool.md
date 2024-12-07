---
title: Legacy Sound Manager (sound_pool.nvgt)
url: docs/references_include_legacy_sound_manager_sound_pool.html
---

<h1>Legacy Sound Manager (sound_pool.nvgt)</h1>
<h2>Classes</h2>
<h3>sound_pool</h3>
<p>This class provides a convenient way of managing sounds in an environment, with 1 to 3 dimensions. The sound_pool_item class holds all the information necessary for one single sound in the game world. Note that you should not make instances of the sound_pool_item class directly but always use the methods and properties provided in the sound_pool class.</p>
<p><code>sound_pool(int default_item_size = 100);</code></p>
<h4>Arguments:</h4>
<ul>
<li>int default_item_size = 100: the number of sound items to be initialized by default.</li>
</ul>
<h4>Methods</h4>
<h5>destroy_all</h5>
<p>destroy all sounds.</p>
<p><code>void sound_pool::destroy_all();</code></p>
<h5>destroy_sound</h5>
<p>Destroy a sound.</p>
<p><code>bool sound_pool::destroy_sound(int slot);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to destroy.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is removed successfully, false otherwise.</p>
<h5>pause_all</h5>
<p>Pauses all sounds.</p>
<p><code>void sound_pool::pause_all();</code></p>
<h5>pause_sound</h5>
<p>Pauses the sound.</p>
<p><code>bool sound_pool::pause_sound(int slot);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the sound slot you wish to pause.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound was paused, false otherwise.</p>
<h5>play_1d</h5>
<p>Play a sound in 1 dimension and return a slot.</p>
<p><code>int sound_pool::play_1d(string filename, pack@ packfile, float listener_x, float sound_x, bool looping, bool persistent = false);</code></p>
<h6>Arguments:</h6>
<ul>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use. This can be omitted.</li>
<li>float listener_x: the listener coordinates in X form.</li>
<li>float sound_x: the coordinates of the sound in X form.</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the sound which can be modified later, or -1 if error. This method may return -2 if the sound is out of earshot.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up if it is not set to be persistent.</p>
<h5>play_2d</h5>
<p>Play a sound in 2 dimensions and return a slot.</p>
<ol>
<li><code>int sound_pool::play_2d(string filename, pack@ packfile, float listener_x, float listener_y, float sound_x, float sound_y, bool looping, bool persistent = false);</code></li>
<li><code>int sound_pool::play_2d(string filename, pack@ packfile, float listener_x, float listener_y, float sound_x, float sound_y, double rotation, bool looping, bool persistent = false);</code></li>
<li><code>int sound_pool::play_2d(string filename, float listener_x, float listener_y, float sound_x, float sound_y, bool looping, bool persistent = false);</code></li>
<li><code>int sound_pool::play_2d(string filename, float listener_x, float listener_y, float sound_x, float sound_y, double rotation, bool looping, bool persistent = false);</code></li>
</ol>
<h6>Arguments:</h6>
<ul>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use (optional).</li>
<li>float listener_x, listener_y: the listener coordinates in X, Y form.</li>
<li>float sound_x, sound_y: the coordinates of the sound in X, Y form.</li>
<li>double rotation: the listener's rotation (optional).</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the sound which can be modified later, or -1 if error. This method may return -2 if the sound is out of earshot.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up if it is not set to be persistent.</p>
<h5>play_3d</h5>
<p>Play a sound in 3 dimensions and return a slot.</p>
<ol>
<li><code>int sound_pool::play_3d(string filename, pack@ packfile, float listener_x, float listener_y, float listener_z, float sound_x, float sound_y, float sound_z, double rotation, bool looping, bool persistent = false);</code></li>
<li><code>int sound_pool::play_3d(string filename, pack@ packfile, vector listener, vector sound_coordinate, double rotation, bool looping, bool persistent = false);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use. This can be omitted</li>
<li>float listener_x, listener_y, listener_z: the listener coordinates in X, Y, Z form.</li>
<li>float sound_x, sound_y, sound_z: the coordinates of the sound in X, Y, Z form.</li>
<li>double rotation: the listener's rotation.</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use. This can be omitted</li>
<li>vector listener: the coordinates of listener in vector form.</li>
<li>vector sound_coordinate: the coordinates of the sound in vector form.</li>
<li>double rotation: the listener's rotation.</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the sound which can be modified later, or -1 if error. This method may return -2 if the sound is out of earshot.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up if it is not set to be persistent.</p>
<h5>play_extended</h5>
<p>Play a sound and return a slot. This method has many parameters that can be customized.</p>
<p><code>int sound_pool::play_extended(int dimension, string filename, pack@ packfile, float listener_x, float listener_y, float listener_z, float sound_x, float sound_y, float sound_z, double rotation, int left_range, int right_range, int backward_range, int forward_range, int lower_range, int upper_range, bool looping, double offset, float start_pan, float start_volume, float start_pitch, bool persistent = false, mixer@ mix = null, string[]@ fx = null, bool start_playing = true, double theta = 0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int dimension: the number of dimension to play on, 1, 2, 3.</li>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use.</li>
<li>float listener_x, listener_y, listener_z: the listener coordinates in X, Y, Z form.</li>
<li>float sound_x, sound_y, sound_z: the coordinates of the sound in X, Y, Z form.</li>
<li>double rotation: the listener's rotation.</li>
<li>int left_range, right_range, backward_range, forward_range, lower_range, upper_range: the range of the sound.</li>
<li>bool looping: should the sound play continuously?</li>
<li>double offset: the number of milliseconds for the sound to start playing at.</li>
<li>float start_pan: the pan of the sound. -100 is left, 0 is middle, and 100 is right.</li>
<li>float start_volume: the volume of the sound. 0 is maximum and -100 is silent.</li>
<li>float start_pitch: the pitch of the sound.</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
<li>mixer@ mix = null: the mixer to attach to this sound.</li>
<li>string[]@ fx = null: array of effects to be set.</li>
<li>bool start_playing = true: should the sound play the moment this function is executed?</li>
<li>double theta = 0: the theta calculated by <code>calculate_theta</code> function in rotation.nvgt include.</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the sound which can be modified later, or -1 if error. This method may return -2 if the sound is out of earshot.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up if it is not set to be persistent.</p>
<h5>play_stationary</h5>
<p>Play a stationary sound and return a slot.</p>
<ol>
<li><code>int sound_pool::play_stationary(string filename, bool looping, bool persistent = false);</code></li>
<li><code>int sound_pool::play_stationary(string filename, pack@ packfile, bool looping, bool persistent = false);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>string filename: the file to play.</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>string filename: the file to play.</li>
<li>pack@ packfile: the pack to use.</li>
<li>bool looping: should the sound play continuously?</li>
<li>bool persistent = false: should the sound be cleaned up once the sound is finished playing?</li>
</ul>
<h6>Returns:</h6>
<p>int: the index of the sound which can be modified later, or -1 if error. This method may return -2 if the sound is out of earshot.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up if it is not set to be persistent.</p>
<p>This method will play the sound in stationary mode. This means that sounds played by this method have no movement updates as if they are stationary, and coordinate update functions will not work.</p>
<h5>resume_all</h5>
<p>Resumes all sounds.</p>
<p><code>void sound_pool::resume_all();</code></p>
<h5>resume_sound</h5>
<p>Resumes the sound.</p>
<p><code>bool sound_pool::resume_sound(int slot);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the sound slot you wish to resume.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound was resumed, false otherwise.</p>
<h5>sound_is_active</h5>
<p>Determine whether the sound is active.</p>
<p><code>bool sound_pool::sound_is_active(int slot);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the sound slot you wish to check.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is active, false otherwise.</p>
<h6>Remarks:</h6>
<p>If the looping parameter is set to true and the sound object is inactive, the sound is still considered to be active as this just means that we are currently out of earshot. A non-looping sound that has finished playing is considered to be dead, and will be cleaned up.</p>
<h5>sound_is_playing</h5>
<p>Determine whether the sound is playing.</p>
<p><code>bool sound_pool::sound_is_playing(int slot);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the sound slot you wish to check.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is playing, false otherwise.</p>
<h5>update_listener_1d</h5>
<p>Updates the listener coordinate in 1 dimension.</p>
<p><code>void sound_pool::update_listener_1d(float listener_x);</code></p>
<h6>Arguments:</h6>
<ul>
<li>float listener_x: the X coordinate of the listener.</li>
</ul>
<h5>update_listener_2d</h5>
<p>Updates the listener coordinate in 2 dimensions.</p>
<p><code>void sound_pool::update_listener_2d(float listener_x, float listener_y, double rotation = 0.0);</code></p>
<h6>Arguments:</h6>
<ul>
<li>float listener_x: the X coordinate of the listener.</li>
<li>float listener_y: the Y coordinate of the listener.</li>
<li>double rotation = 0.0: the rotation to use.</li>
</ul>
<h5>update_listener_3d</h5>
<p>Updates the listener coordinate in 3 dimensions.</p>
<ol>
<li><code>void sound_pool::update_listener_3d(float listener_x, float listener_y, float listener_z, double rotation = 0.0, bool refresh_y_is_elevation = true);</code></li>
<li><code>void sound_pool::update_listener_3d(vector listener, double rotation = 0.0, bool refresh_y_is_elevation = true);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>float listener_x: the X coordinate of the listener.</li>
<li>float listener_y: the Y coordinate of the listener.</li>
<li>float listener_z: the Z coordinate of the listener.</li>
<li>double rotation = 0.0: the rotation to use.</li>
<li>bool refresh_y_is_elevation = true: toggles whether <code>y_is_elevation</code> property should refresh from the <code>sound_pool_default_y_is_elevation</code> global property.</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>vector listener: the coordinates of the listener in vector form.</li>
<li>double rotation = 0.0: the rotation to use.</li>
<li>bool refresh_y_is_elevation = true: toggles whether <code>y_is_elevation</code> property should refresh from the <code>sound_pool_default_y_is_elevation</code> global property.</li>
</ul>
<h5>update_sound_1d</h5>
<p>Updates the sound coordinate in 1 dimensions.</p>
<p><code>bool sound_pool::update_sound_1d(int slot, int x);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int x: the X coordinate of the sound.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_2d</h5>
<p>Updates the sound coordinate in 2 dimensions.</p>
<p><code>bool sound_pool::update_sound_2d(int slot, int x, int y);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int x: the X coordinate of the sound.</li>
<li>int y: the Y coordinate of the sound.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_3d</h5>
<p>Updates the sound coordinate in 3 dimensions.</p>
<ol>
<li><code>bool sound_pool::update_sound_3d(int slot, int x, int y, int z);</code></li>
<li><code>bool sound_pool::update_sound_3d(int slot, vector coordinate);</code></li>
</ol>
<h6>Arguments (1):</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int x: the X coordinate of the sound.</li>
<li>int y: the Y coordinate of the sound.</li>
<li>int z: the Z coordinate of the sound.</li>
</ul>
<h6>Arguments (2):</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>vector coordinate: the coordinate of the sound in vector form.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_range_1d</h5>
<p>Updates the sound range in 1 dimensions.</p>
<p><code>bool sound_pool::update_sound_range_1d(int slot, int left_range, int right_range);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int left_range: the left range to update.</li>
<li>int right_range: the right range to update.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_range_2d</h5>
<p>Updates the sound range in 2 dimensions.</p>
<p><code>bool sound_pool::update_sound_range_2d(int slot, int left_range, int right_range, int backward_range, int forward_range);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int left_range: the left range to update.</li>
<li>int right_range: the right range to update.</li>
<li>int backward_range: the backward range to update.</li>
<li>int forward_range: the forward range to update.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_range_3d</h5>
<p>Updates the sound range in 3 dimensions.</p>
<p><code>bool sound_pool::update_sound_range_3d(int slot, int left_range, int right_range, int backward_range, int forward_range, int lower_range, int upper_range, bool update_sound = true);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>int left_range: the left range to update.</li>
<li>int right_range: the right range to update.</li>
<li>int backward_range: the backward range to update.</li>
<li>int forward_range: the forward range to update.</li>
<li>int lower_range: the bottom / lower range to update.</li>
<li>int upper_range: the above / upper range to update.</li>
<li>bool update_sound = true: toggles whether all the sound will be updated automatically.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h5>update_sound_start_values</h5>
<p>Updates the sound start properties.</p>
<p><code>bool sound_pool::update_sound_start_values(int slot, float start_pan, float start_volume, float start_pitch);</code></p>
<h6>Arguments:</h6>
<ul>
<li>int slot: the slot of the sound you wish to update.</li>
<li>float start_pan: the new pan to update.</li>
<li>float start_volume: the new volume to update.</li>
<li>float start_pitch: the new pitch to update.</li>
</ul>
<h6>Returns:</h6>
<p>bool: true if the sound is updated successfully, false otherwise.</p>
<h4>Properties</h4>
<h5>behind_pitch_decrease</h5>
<p>The pitch step size to decrease when the sound is behind. Default is 0.25.</p>
<p><code>float sound_pool::behind_pitch_decrease;</code></p>
<h5>max_distance</h5>
<p>The maximum distance that the sounds can be heard. Default is 0 (disabled).</p>
<p><code>int sound_pool::max_distance;</code></p>
<h5>pan_step</h5>
<p>The pan step size, the sound's final pan or position in HRTF is calculated by multiplying the player's distance from the sound by this value. Default is 1.0.</p>
<p><code>float sound_pool::pan_step;</code></p>
<h5>volume_step</h5>
<p>The volume step size, the sound's final volume is subtracted by this number multiplied by the player's distance from the sound. Default is 1.0.</p>
<p><code>float sound_pool::volume_step;</code></p>
<h5>y_is_elevation</h5>
<p>Toggles whether the Y coordinate is the same as Z, or in otherwords whether the y coordinate determines up/down or forward/backwards in your game world. By default, it retrieves from the <code>sound_pool_default_y_elevation</code> global property.</p>
<p><code>bool sound_pool::y_is_elevation = sound_pool_default_y_elevation;</code></p>
