# WavefrontCodeStreamProbe
A simple Wavefront Probe written for a CodeStream pipeline (SSH task), that checks if an alert was triggered. This is useful for CodeStream instances that sit behind a firewall (pull mechanism).

# Requirements / Assumptions
This script assumes you have the following environment variables set:
- WFPAUTH (for your Wavefront API token)
- WFPEVENTID (the unique alert ID that you're probing for... this is found in wavefront UI by selecting the alert in question and grabbing the # after "../alerts/#")
- WFPBASEURL (ex: surf.wavefront.com ... do not include "/")

This also assumes the script is ran in a CodeStream ssh task, which requires you to run the following commands _before_ you execute this python script:
```
export WFPAUTH=[API TOKEN]
export WFPEVENTID=[ALERT'S ID]
export WFPBASEURL=$ [x.wavefront.com]
export RESPONSE=$SCRIPT_RESPONSE_FILE
```

# Output
The preceeding CodeStream tasks can then check the response file for the SSH task that this script is ran in for FIRING (aka alert was triggered). Otherwise it will say "NORMAL" after 4 minutes (tunable by changing loop count and/or sleep count)

Example "condition": `$(Push to Prod.Wavefront Probe.output.response} == "FIRING"`
