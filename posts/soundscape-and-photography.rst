.. title: Soundscape and Photography
.. slug: soundscape-and-photography
.. date: 2015-09-09 07:03:49 UTC+02:00
.. tags: soundscape, photography, exhibition
.. link:
.. description: Soundscape and Photography. How to build a soundscape to improve immersion in a photographic exhibition.
.. type: text
.. author: Alexandre Dulaunoy

.. figure:: train.jpg

   Every second is the beginning of something, ƒ/2.0, 35mm, train_ on flickr

.. _train: https://www.flickr.com/photos/adulau/17450085919

One year ago, the opportunity of doing an exhibition helps me to experiment something new with photography. In some past exhibition, I
had the impression that some viewers cannot be immersed due to surrounding sounds (e.g. noisy environment or people talking too loud).
The idea was to enrich my artwork with a soundscape supporting the viewers' feelings. The soundscape will be there to limit the
overall noise disruption from the exhibition. The experiment looks fun to do and I try to document my journey to build a soundscape
to support my photographs.

My theme for the exhibition was the train and I already selected a series of photos. Based on this photographic material, I draw some
indicators that could be used as key elements or references for the viewers.

* Sounds of train starts (1)
* Sounds of train stops (2)
* Environmental sounds of train (e.g. doors(3), railways(4), people talking(5), ...)
* Vocal announces inside or outside (6)

Having these in mind, I recorded sounds during some trips in various trains or train stations in Belgium. I had the luck to borrow a `Zoom H6 Six-Track Portable Recorder <http://www.amazon.com/dp/B00DFU9BRK>`_ from a very kind colleague. Recording in public spaces is not so far from photography. The difficulty is the sound framing. Where you need to highlight a specific element in the sound and discard the rest. I was not used to record sounds, so it was pretty new to me. Similarities with the act of photography are interesting, being alone, avoid distracting elements in your frame or record the right instant.

After 3 months of recording raw materials (don't forget to limit level and record in raw WAV/PCM format), I did a selection of the sounds (`another similarity with photography 'select or die' <http://www.foo.be/photoblog/posts/select-or-die.html>`_). I classify the samples to use in loops and the others which are longer samples. What's the process to create a coherent soundscape for the `photo set <https://www.flickr.com/photos/adulau/albums/72157652166570610>`_. I wanted to recall the train atmosphere were you have some kind of monotonous sounds but which shouldn't be boring and tend to be forgot after a certain number of repetitions.

So I started with the loops, this is an art in itself. While listening to the raw materials, I selected some repetitive sound patterns. From the each of the selected repetitive pattern, I cut some seconds that could be repeated to reproduce the original sound patterns of the raw sample. The seconds selected should be clear without distracting noises. Then you can create the loops, tests it (keep the loop playing and listen) and save it (still in raw WAV/PCM format or FLAC). For this process, I used `Audacity <http://audacityteam.org/>`_ which is a simple but advanced free software to edit audio samples. The software includes functionality like finding the `zero crossing point <http://manual.audacityteam.org/o/man/edit_menu.html#zero>`_ to have smooth transition in the loops.

After the creation of the audio loops (4 and 4bis), I had long samples with some specific element like doors closing(3), train starting(1) or stopping(2), vocal announces(6). How can I play all these samples sequentially and find an accurate pattern for my photo sets? I tried some audio software to do that but these are often huge and utterly complex to use (e.g. you need to use a graphical user interface to shuffle a list of sample for each experiment). I end up using `bash <https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29>`_ and `SoX <http://sox.sourceforge.net/>`_ to do the composition. This approach helps to focus on the content and just write some lines of shell script to create my soundscape.

The whole play script used for the soundscape written in Bash shell and using SoX:

.. code-block:: bash

        #!/bin/bash

        looprepeat="7"
        fadeout="fade t 0 0 3"
        LONGSLEEP=40
        SHORTSLEEP=10
        VSSLEEP=5

        while [ true ]
        do
                play BelgianTrainLoopOK2.flac repeat $looprepeat $fadeout; play BelgianTrainAnotherStopOK.flac $fadeout
                sleep $SHORTSLEEP
                play BelgianAnnounceBruxelles.flac $fadeout
                sleep $SHORTSLEEP
                play BelgianNewLTrainStart.flac $fadeout
                sleep $SHORTSLEEP
                play BelgianTrainLoop2.flac repeat $looprepeat $fadeout
                sleep $SHORTSLEEP
                play Arlon-to-Marbehan.flac $fadeout
                sleep $VSSLEEP
                play BelgianTrainDoorClosing.flac $fadeout
        done

I also did a `quick visualization of each samples <http://www.foo.be/art/audio-cuestart2015/output.png>`_ to find out any glitches or issue that cannot be directly spot by listening. The above script runs during the exhibition and based on the mood of the day, you can change the parameters (time between samples) or the order of the samples.

Not sure if my first experiment is a success but I had interesting feedback during the exhibition. An old lady told me that remembers her when she took the train with her parents. Some where indeed more attentive to the photos or came back when they started to hear the soundscape. And another funny discussion was a guy working at the national train company in Belgium who remembered the exact model of the train.

The overall soundscape including samples and scripts `are freely available under a BSD 2-Clause License <http://www.foo.be/art/audio-cuestart2015/>`_.

