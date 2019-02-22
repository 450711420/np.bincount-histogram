# np.bincount-histogram
N = 15      # size of patch K = 9       # number of prototypes for kmeans P = 20000   # number of randomly selected patches  R = gim.shape[0]    # number of rows in image C = gim.shape[1]    # number of columns in image  X = np.zeros((P,N*N),dtype=float) # initialise array for random patches  for i in range(0, P):     r = random.randint(0,R-N)     c = random.randint(0,C-N)     patch = gim[r:r+N,c:c+N]      X[i,:] = np.reshape(patch,(-1))  codebook, distortion = vq.kmeans(X,K)  spn = np.ceil(np.sqrt(K))    # size of subplot display norm = colors.Normalize(vmin=codebook.min(), vmax=codebook.max())    # set gray range from minimum to maximum for i in range(0,K):     plt.subplot(spn,spn,i+1)     plt.imshow(np.reshape(codebook[i,:],(N,N)),cmap='gray',norm=norm)     plt.gca().add_patch(patches.Circle((2,2), radius=1, color=plt.cm.tab20(i)))     plt.axis('off')    # turn off the axes      X = np.zeros(((R-N)*(C-N),N*N),dtype=float)   # initialise array for all patches i=0 for r in range(0,R-N):     for c in range(0,C-N):         X[i,:] = np.reshape(gim[r:r+N,c:c+N],(-1))         i=i+1  code, dist = vq.vq(X,codebook) code = np.reshape(code,(R-N,C-N))    # reshape the 1D code array into the original 2D image shape  # to give each label a unique colour, turn off normalisation in order to index directly into discrete colour map plt.figure() norm = colors.NoNorm() plt.imshow(code, cmap='tab20', norm=norm) plt.axis('off')    # turn off the axes
