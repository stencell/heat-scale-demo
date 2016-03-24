# heat-scale-demo
Demo to show how heat can provide scaling URLs to allow for external app to control up/down scaling.

- Edit the environment file:
- vi heat-scale-demo/hpc.env  - ensure the values here will work in your environment
- Build the cluster:
heat stack-create hpc-demo -e heat-scale-demo/hpc.env -f heat-scale-demo/build-cluster.yaml 

- Get the scaling handles :
 heat output-show br1 scale_down_url
 heat output-show br1 scale_up_url

"http://10.12.32.10:8000/v1/signal/arn%3Aopenstack%3Aheat%3A%3A9208ac9862d64dffb4972247656d2042%3Astacks%2Fbr1%2F4a10ed31-840e-4552-89f4-87de136c0edc%2Fresources%2Fscale_up_policy?Timestamp=2016-03-24T15%3A23%3A57Z&SignatureMethod=HmacSHA256&AWSAccessKeyId=c4a916d623ef4b0fae7f92ca8de4cd93&SignatureVersion=2&Signature=x%2F34XYveeFsm2q9Zot%2FLM8CQO2JN3Pjjm4qx2iIvsIw%3D"

Then use curl to scale up:  ( use the output on your own stack - don't copy this )
curl -X POST "http://10.12.32.10:8000/v1/signal/arn%3Aopenstack%3Aheat%3A%3A9208ac9862d64dffb4972247656d2042%3Astacks%2Fbr1%2F4a10ed31-840e-4552-89f4-87de136c0edc%2Fresources%2Fscale_up_policy?Timestamp=2016-03-24T15%3A23%3A57Z&SignatureMethod=HmacSHA256&AWSAccessKeyId=c4a916d623ef4b0fae7f92ca8de4cd93&SignatureVersion=2&Signature=x%2F34XYveeFsm2q9Zot%2FLM8CQO2JN3Pjjm4qx2iIvsIw%3D"
