# A GPU-powered Pi for more efficient AI?

[Youtube link](https://www.youtube.com/watch?v=AyR7iCS7gNI)

The Raspberry Pi is a compelling low-power option for running GPU-accelerated LLMs locally.

For my main test setup, here's the hardware I used (some links are affiliate links):

Raspberry Pi 5 8GB ($80): https://www.raspberrypi.com/products/...
Raspberry Pi 27W Power Supply ($14): https://www.raspberrypi.com/products/...
1TB USB SSD ($64): https://amzn.to/3OjJysQ
Pineboards HatDrive! Bottom ($20): https://amzn.to/3Zbz0T5
JMT M.2 Key to PCIe eGPU Dock ($55): https://amzn.to/4eCpi0g
OCuLink cable ($20): https://amzn.to/3YTXNJW
Lian-Li SFX 750W PSU ($130): https://amzn.to/48T4a4R
AMD RX 6700 XT ($400): https://amzn.to/3UXywgI

And here are the resources I mentioned for setting up your own GPU-accelerated Pi:

Blog post with AMD GPU setup instructions: https://www.jeffgeerling.com/blog/202...
Blog post with llama.cpp Vulkan instructions: https://www.jeffgeerling.com/blog/202...
Llama Benchmarking issue: https://github.com/geerlingguy/ollama...
AMD not supporting ROCm on Arm: https://github.com/ROCm/ROCm/issues/3960
Raspberry Pi PCIe Database: https://pipci.jeffgeerling.com
Home Assistant Voice Control: https://www.home-assistant.io/voice_c...
