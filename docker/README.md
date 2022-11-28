Build the container with the following command:
```
docker build -t mltools-demo .
```

Then run the container while forwarding ports 8000 (VSCode server)
Make sure you are under the `docker` directory

```
docker run  --rm --name  demo_container --rm --network host --gpus all -it -v $PWD/../project:/workspace/project -w /workspace/project mltools-demo
```

Upon entering the container, run the following to lanuch the two services:
```
bash entry.sh
```

This would start a tmux session containing two panes for the two services respectively.
Note that the default password to access VSCode server is `centml`.

