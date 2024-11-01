---
title: Assignment 
layout: post
description: An introductory example of Frontend talking to Backend Java application serving jokes.  
---

<script type="module">
  import { javaURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

  const url = `${javaURI}/api/assignments`;
  const addURL = url + "/add";  // haha reaction

  const postOptions = {...fetchOptions,
    method: 'POST',
  };

  fetch(getURL,fetchOptions)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          error('GET API response failure: ' + response.status);
          return;
      }

</script>