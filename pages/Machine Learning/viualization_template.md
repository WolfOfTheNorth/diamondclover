type: "SNIPPET_NOTE"
folder: "ca803f222493d2f21dfd"
title: "Visulaization Template"
description: "Visulaization Template "
snippets: [
  {
    name: ""
    mode: "text"
    content: '''
      import matplotlib.pyplot as plt
      
      
      # Simple scatter plot of data + regressor Model
      plt.scatter(X, y, color='red')
      plt.plot(X, regressor.predict(X), color= 'blue')
      plt.title('Title of my Model)
      plt.xlabel('X Axis Title')
      plt.ylabel('Y Axis Title')
      plt.show()
      
      # HIGH RESOLUTION AND SMOOTHER CURVE
      X_grid = np.arrange(min(X), max(X), 0.1)
      X_grid = X_grid.reshape((len(X_grid), 1))
      plt.scatter(X, y, color='red')
      plt.plot(X_grid, regressor.predict(X_grid), color = 'blue')
      plt.title('Title of my Model)
      plt.xlabel('X Axis Title')
      plt.ylabel('Y Axis Title')
      plt.show()
    '''
  }
]
tags: []
isStarred: false
createdAt: "2017-06-05T15:38:47.303Z"
updatedAt: "2017-06-05T16:03:58.929Z"
