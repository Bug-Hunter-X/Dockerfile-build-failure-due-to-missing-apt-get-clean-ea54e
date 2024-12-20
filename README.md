# Dockerfile Bug: Missing `apt-get clean`

This repository demonstrates a common error in Dockerfiles: forgetting to run `apt-get clean` after installing packages. This can lead to significantly slower build times and larger image sizes.

## Bug

The original `Dockerfile` (in `Dockerfile`) installs Python and its dependencies but neglects to clean up the downloaded packages. This results in bloated image layers.

## Solution

The `Dockerfile-solution` demonstrates the correct way of building a Docker image by adding `apt-get clean` and `apt-get autoremove`  to remove unneeded packages.

## How to Reproduce

1. Clone this repository.
2. Build the original `Dockerfile` using `docker build -t buggy-image -f Dockerfile .`
3. Observe the build time and image size.
4. Build the fixed `Dockerfile-solution` using `docker build -t fixed-image -f Dockerfile-solution .`
5. Compare the build time and image size. You'll notice a significant improvement in both.

## Lessons Learned

Always remember to run `apt-get clean` and optionally `apt-get autoremove` after installing packages in your `Dockerfile`. This will keep your images small and your builds fast.