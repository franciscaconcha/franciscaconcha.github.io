---
layout: default
title: Research
permalink: research
---
# Current PhD research
We know that most stars are born in clustered environments in molecular clouds, high in both stellar and gas densities. These are also the surroundings where circumstellar disks form around young stars. Planetary systems form in said disks. However, the hostile environments during the first millions years of evolution of stellar clusters can dramatically affect the evolution of the circumstellar disks: they might get truncated by dynamical interactions with other nearby stars, they might get stripped of their material due to the ram pressure of the intracluster gas that surrounds them, they might get evaporated due to the intense radiation from their host or neighbouring stars, among many other processes. The disks also present their own internal viscous evolution, which leads them to grow and evolve through time. Some of these physical processes are probably more dominant than others, affecting the evolution of circumstellar disks more strongly. Also, different mechanisms may dominate during different stages of the cluster's evolution. Understanding the processes that occur inside young stellar clusters will help us understand circumstellar disks and, eventually, planetary formation.

The research I'm currently carrying out during my PhD looks to anwser many questions, among them: what are the main mechanisms affecting the evolution of circumstellar disks around stars in young clusters? From this, I also look to get insights about how our Solar System was formed. The way in which I am trying to tackle this problem is through the use of computational simulations. I run simulations of young stellar clusters using AMUSE, the Astrophysical Multipurpose Software Environment, a community effort with the main development by the AMUSE team at Leiden Observatory under supervision of Simon Portegies Zwart. In these simulations I consider the different processes that might be affecting the evolution of the circumstellar disks, and then analyze the resulting size distributions of the disks and other characteristics of the cluster.

We are lucky to be living in an era where we have poweful telescopes looking at the sky. Nowadays, thanks to enormous observational installations such as ALMA, it is possible to observe circumstellar disks inside their formation environments. Comparing these observations against simulation results offers an invaluable standard to measure if our research assumptions are leading us in the right direction.

# Research for my M.Sc. in Computer Science
Astronomy is a data-intensive discipline, where Terabytes of information are being produced around the world every night. Quick processing and analysis of said data is crucial for the development of scientific results. Because of this, the pipelines of data processing tools for astronomy are beginning to embrace the Big Data paradigms. However, hardware-wise, there are also ways to accelerate algorithms for data analysis.

During my Master's program in Computer Science I developed a tool for astronomical data reduction and photometric lightcurve obtention using GPU-accelerated algorithms. The GPU is the Graphics Processing Unit of a computer, and in the last decades the use of GPUs for accelerating mathematical calculations has become standard in many data-intensive areas. The design of the GPU allows for many calculations to be carried out in parallel, thus accelerating the execution times of algorithms sometimes for factors of two orders of magnitude, compare to their CPU counterparts.

However, designing data-intensive algorithms for the GPU is not straight-forward. You cannot just run your CPU scripts on a GPU, the whole problem needs to be re-thought and re-designed to take advantage of the GPU's hardware.

You can read my thesis (in English), to get more insights about the algorithms I designed, here.
