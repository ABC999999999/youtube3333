cmake_minimum_required(VERSION 3.14)

set(CMAKE_CXX_STANDARD 11)

project(youtube)

include(FetchContent)
FetchContent_Declare(
  googletest
  # Specify the commit you depend on and update it regularly.
  URL https://github.com/google/googletest/archive/53495a2a7d6ba7e0691a7f3602e9a5324bba6e45.zip
)

set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
include(GoogleTest)

if(MSVC)
  add_compile_options(/Wall)
else()
  add_compile_options(
      -Wall
      -Wextra
      -pedantic
      # Below is to avoid unnecessary warnings before code is implemented.
      -Wno-unused-parameter)
endif()

file(COPY src/videos.txt DESTINATION src/)

add_library(youtube_lib
    src/commandparser.cpp
    src/commandparser.h
    src/helper.cpp
    src/helper.h
    src/video.cpp
    src/video.h
    src/videolibrary.cpp
    src/videolibrary.h
    src/videoplayer.cpp
    src/videoplayer.h
    src/videoplaylist.h
    src/videoplaylist.cpp)

add_executable(youtube src/main.cpp)
target_link_libraries(youtube youtube_lib)

enable_testing()

add_executable(part1_test test/part1_test.cpp)
target_link_libraries(part1_test youtube_lib gmock gtest gtest_main)
gtest_discover_tests(part1_test)

add_executable(part2_test test/part2_test.cpp)
target_link_libraries(part2_test youtube_lib gmock gtest gtest_main)
gtest_discover_tests(part2_test)

add_executable(part3_test test/part3_test.cpp)
target_link_libraries(part3_test youtube_lib gmock gtest gtest_main)
gtest_discover_tests(part3_test)

add_executable(part4_test test/part4_test.cpp)
target_link_libraries(part4_test youtube_lib gmock gtest gtest_main)
gtest_discover_tests(part4_test)

add_executable(videolibrary_test test/videolibrary_test.cpp)
target_link_libraries(videolibrary_test youtube_lib gmock gtest gtest_main)
gtest_discover_tests(videolibrary_test)
YT> NUMBER_OF_VIDEOS
5 videos in the library
YT> SHOW_ALL_VIDEOS
Here's a list of all available videos:
Amazing cats (amazing_cats_video_id) [#cat #animal]
Another Cat Video (another_cat_video_id) [#cat #animal]
Funny Dogs (funny_dogs_video_id) [#dog #animal]
Life at Google (life_at_google_video_id) [#google #career]
Video about nothing (nothing_video_id) []
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> PLAY funny_dogs_video_id
Stopping video: Amazing Cats
Playing video: Funny Dogs
YT> PLAY funny_dogs_video_id
Stopping video: Funny Dogs
Playing video: Funny Dogs
YT> PLAY some_other_video_id
Cannot play video: Video does not exist
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> STOP
Stopping video: Amazing Cats
YT> STOP
Cannot stop video: No video is currently playing
YT> PLAY_RANDOM
Playing video: Life at Google
YT> PLAY_RANDOM
Stopping video: Life at Google
Playing video: Funny Dogs
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> PAUSE
Pausing video: Amazing Cats
YT> PAUSE
Video already paused: Amazing Cats
YT> STOP
Stopping video: Amazing Cats
YT> PAUSE
Cannot pause video: No video is currently playing
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> PAUSE
Pausing video: Amazing Cats
YT> PLAY another_cat_video_id
Stopping video: Amazing Cats
Playing video: Another Cat Video
YT> PAUSE
Pausing video: Another Cat Video
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> CONTINUE
Cannot continue video: Video is not paused
YT> PAUSE
Pausing video: Amazing Cats
YT> CONTINUE
Continuing video: Amazing Cats
YT> CONTINUE
Cannot continue video: Video is not paused
YT> STOP
Stopping video: Amazing Cats
YT> CONTINUE
Cannot continue video: No video is currently playing
YT> PLAY amazing_cats_video_id
Playing video: Amazing Cats
YT> SHOW_PLAYING
Currently playing: Amazing Cats (amazing_cats_video_id) [#cat #animal]
YT> PAUSE
Pausing video: Amazing Cats
YT> SHOW_PLAYING
Currently playing: Amazing Cats (amazing_cats_video_id) [#cat #animal] - PAUSED
YT> STOP
Stopping video: Amazing Cats
YT> SHOW_PLAYING
No video is currently playing
YT> CREATE_PLAYLIST my_PLAYlist
Successfully created new playlist: my_PLAYlist
YT> CREATE_PLAYLIST my_PLAYLIST
Cannot create playlist: A playlist with the same name already exists
YT> CREATE_PLAYLIST my_playLIST
Successfully created new playlist: my_playLIST
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> ADD_TO_PLAYLIST my_PLAYlist amazing_cats_video_id
Cannot add video to my_PLAYlist: Video already added
YT> ADD_TO_PLAYLIST my_playlist some_other_video_id
Cannot add video to my_playlist: Video does not exist
YT> ADD_TO_PLAYLIST another_playlist some_other_video_id
Cannot add video to another_playlist: Playlist does not exist
YT> SHOW_ALL_PLAYLISTS
No playlists exist yet
YT> CREATE_PLAYLIST MY_playlist
Successfully created new playlist: MY_playlist
YT> SHOW_ALL_PLAYLISTS
Showing all playlists:
MY_playlist
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> SHOW_PLAYLIST my_PLAYLIST
Showing playlist: my_PLAYLIST
No videos here yet
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> SHOW_PLAYLIST my_playlist
Showing playlist: my_playlist
Amazing Cats (amazing_cats_video_id) [#cat #animal]
YT> SHOW_PLAYLIST another_playlist
Cannot show playlist another_playlist: Playlist does not exist
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> ADD_TO_PLAYLIST my_PLAYlist amazing_cats_video_id
Added video to my_PLAYlist: Amazing Cats
YT> REMOVE_FROM_PLAYLIST my_playLIST amazing_cats_video_id
Removed video from my_playLIST: Amazing Cats
YT> REMOVE_FROM_PLAYLIST my_playlist amazing_cats_video_id
Cannot remove video from my_playlist: Video is not in playlist
YT> REMOVE_FROM_PLAYLIST my_playlist some_other_video_id
Cannot remove video from my_playlist: Video does not exist
YT> REMOVE_FROM_PLAYLIST another_playlist amazing_cats_video_id
Cannot remove video from another_playlist: Playlist does not exist
YT> REMOVE_FROM_PLAYLIST another_playlist some_other_video_id
Cannot remove video from another_playlist: Playlist does not exist
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> CLEAR_PLAYLIST my_playlist
Successfully removed all videos from my_playlist
YT> SHOW_PLAYLIST my_playlist
Showing playlist: my_playlist
No videos here yet.
YT> CLEAR_PLAYLIST another_playlist
Cannot clear playlist another_playlist: Playlist does not exist
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> DELETE_PLAYLIST my_playlist
Deleted playlist: my_playlist
YT> DELETE_PLAYLIST my_playlist
Cannot delete playlist my_playlist: Playlist does not exist
YT> SEARCH_VIDEOS cat
Here are the results for cat:
1) Amazing Cats (amazing_cats_video_id) [#cat #animal]
2) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? If yes, specify the number of the video.
If your answer is not a valid number, we will assume it's a no.
Nope!
YT> SEARCH_VIDEOS cat
Here are the results for cat:
1) Amazing Cats (amazing_cats_video_id) [#cat #animal]
2) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? If yes, specify the number of the video.
If your answer is not a valid number, we will assume it's a no.
2
Playing video: Another Cat Video
YT> SEARCH_VIDEOS blah
No search results for blah
YT> SEARCH_VIDEOS_WITH_TAG #cat
Here are the results for #cat:
1) Amazing Cats (amazing_cats_video_id) [#cat #animal]
2) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? If yes, specify the number of the video.
If your answer is not a valid number, we will assume it's a no.
No
YT> SEARCH_VIDEOS_WITH_TAG #cat
Here are the results for #cat:
1) Amazing Cats (amazing_cats_video_id) [#cat #animal]
2) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? If yes, specify the number of the video.
If your answer is not a valid number, we will assume it's a no.
2
Playing video: Another Cat Video
YT> SEARCH_VIDEOS_WITH_TAG #blah
No search results for #blah
YT> SEARCH_VIDEOS_WITH_TAG cat
No search results for cat
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> FLAG_VIDEO another_cat_video_id
Successfully flagged video: Another Cat Video (reason: Not supplied)
YT> FLAG_VIDEO amazing_cats_video_id
Cannot flag video: Video is already flagged
YT> FLAG_VIDEO video_does_not_exist flag_video_reason
Cannot flag video: Video does not exist
YT> PLAY amazing_cats_video_id
Cannot play video: Video is currently flagged (reason: dont_like_cats)
YT> PLAY another_cat_video_id
Cannot play video: Video is currently flagged (reason: Not supplied)
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Cannot add video to my_playlist: Video is currently flagged (reason:
dont_like_cats)
YT> ADD_TO_PLAYLIST my_playlist another_cat_video_id
Cannot add video to my_playlist: Video is currently flagged (reason:
Not supplied)
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Cannot add video to my_playlist: Video is currently flagged (reason:
dont_like_cats)
YT> FLAG_VIDEO amazing_cats_video_id
Successfully flagged video: Amazing Cats (reason: Not supplied)
YT> FLAG_VIDEO another_cat_video_id
Successfully flagged video: Another Cat Video (reason: Not supplied)
YT> FLAG_VIDEO life_at_google_video_id
Successfully flagged video: Life at Google (reason: Not supplied)
YT> FLAG_VIDEO funny_dogs_video_id
Successfully flagged video: Funny Dogs (reason: Not supplied)
YT> FLAG_VIDEO nothing_video_id
Successfully flagged video: Video about nothing (reason: Not supplied)
YT> PLAY_RANDOM
No videos available
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> SHOW_ALL_VIDEOS
Here's a list of all available videos:
Amazing cats (amazing_cats_video_id) [#cat #animal] - FLAGGED (reason:
dont_like_cats)
Another Cat Video (another_cat_video_id) [#cat #animal]
Funny Dogs (funny_dogs_video_id) [#dog #animal]
Life at Google (google_video_id) [#google #career]
Video about nothing (nothing_video_id) []
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> SHOW_PLAYLIST my_playlist
Showing playlist: my_playlist
Amazing Cats (amazing_cats_video_id) [#cat #animal] - FLAGGED (reason:
dont_like_cats)
YT> SEARCH_VIDEO cat
Here are the results for cat:
1) Amazing Cats (amazing_cats_video_id) [#cat #animal]
2) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? [...]
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> SEARCH_VIDEO cat
Here are the results for cat:
1) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? [...]
YT> SEARCH_VIDEOS_WITH_TAG #cat
Here are the results for #cat:
1) Another Cat Video (another_cat_video_id) [#cat #animal]
Would you like to play any of the above? [...]
YT> PLAY_VIDEO amazing_cats_video_id
Playing video: Amazing Cats
YT> SHOW_PLAYING
Currently playing: Amazing Cats (amazing_cats_video_id) [#cat #animal]
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Stopping video: Amazing Cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> SHOW_PLAYING
No video is currently playing
YT> FLAG_VIDEO amazing_cats_video_id
Successfully flagged video: Amazing Cats (reason: Not supplied)
YT> ALLOW_VIDEO amazing_cats_video_id
Successfully removed flag from video: Amazing Cats
YT> ALLOW_VIDEO amazing_cats_video_id
Cannot remove flag from video: Video is not flagged
YT> ALLOW_VIDEO non_existing_video_id
Cannot remove flag from video: Video does not exist
YT> CREATE_PLAYLIST my_playlist
Successfully created new playlist: my_playlist
YT> ADD_TO_PLAYLIST my_playlist amazing_cats_video_id
Added video to my_playlist: Amazing Cats
YT> FLAG_VIDEO amazing_cats_video_id dont_like_cats
Successfully flagged video: Amazing Cats (reason: dont_like_cats)
YT> SHOW_PLAYLIST my_playlist
Showing playlist: my_playlist
Amazing Cats (amazing_cats_video_id) [#cat #animal] - FLAGGED (reason:
dont_like_cats)
YT> ALLOW_VIDEO amazing_cats_video_id
Successfully removed flag from video: Amazing Cats
YT> SHOW_PLAYLIST my_playlist
Showing playlist: my_playlist
Amazing Cats (amazing_cats_video_id) [#cat #animal]
