---
layout: post
title: Open Todo API
short-description: A site that users can communicate with using JSON.
---

# Summary

This is a site that users can communicate with using JSON.

# Serializers

An important part of this project was serializers. I learned how to define
classes for serializers that each correspond to a model and define how that
model appears as JSON.

# Adding fields

As I progressed through the project, I had to add new fields to the records. I
studied `rails g migration -h` to see how this works. I then changed the
serializers, models, and controllers to match.
