# albatros_firmware_slx

`albatros_dual_snap_4bit (1).slx` is a file that was previously constructed. It does not correspond to fpg file that we currently use but I thought to conain much of the same logic. 

`quad_input_poco.slx` comes from a casper tutorial and is likely the used as a boilerplate for constructing our current firmware. 

`reconstruct_albatros_dual_15.slx` is my attempt to combine the above two slx files and, using the names of registers used by our software, to reverse engineer our currently firmware to retrieve a source file that compiles to something that is functionally identical to what we currently have.

### Known issues

I have tested `reconstruct_albatros_dual_15` on our software but it fails to initialize properly; failing scilently. The bitstream is happy to be written to the FPGA, and our software is able to read/write from/to it's registers. However, when we ask it to report a time-integrated power-spectrum, the data read is all zeros. 

In a previous version of our software, the katcp socket (to my understanding this is the protocol used to by our PI to communicate with the FPGA) times-out consistently after 3 minutes of operating. After the three minutes, I start it up again and tour new firmware bitstream works! This makes me think something is going wrong at the initialization stage. However, this problem does not occur if we use the old bitstream (the one we've been using since 2019), i.e. our firmware boots up reliably. 

In our current software, the katcp socket does not time-out and our new firmware never outputs anything other than zeros, failing scilently. 

**In conclusion**, this leads me to believe that our new simulink file `reconstruct_albatros_dual_15.slx` is almost functional. It just doesn't initialize correctly. I have been unable to fix this bug for over a week and am now soliciting help from the casper community. Any advice or help is welcome. On the CASPER Slack I'm Stephen Fay (stephen.fay@mail.mcgill.ca). 

The crucial parts of the analysis code are the python files in the root: `config_fpga.py` and `albatrosdigitizer.py` (they uses `config.ini`)

