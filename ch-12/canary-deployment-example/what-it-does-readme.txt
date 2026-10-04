# Watch the progress of rollouts
kubectl argo rollouts get rollout rollouts-demo --watch

# Update the rollout
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow

# Check again
kubectl argo rollouts get rollout rollouts-demo --watch

# Promote rollout manually
kubectl argo rollouts promote rollouts-demo

# Check status now
kubectl argo rollouts get rollout rollouts-demo --watch

#######################
### Abort a rollout ###
#######################

# First update to new version
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:red

# This time instead of promoting the rollout to the next step, 
# we will abort the update, so that it falls back to the "stable" version. 

kubectl argo rollouts abort rollouts-demo

# The rollout is still considered Degraded, since the desired version 
# (the red image) is not the version which is actually running
# In order to be healthy again
# Set image command using the previous, "yellow" image.

kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow





