Information Gain = H(P_node) - W_left * H(P_left) + W_right * H(P_right)

H is the entropy. Note that H takes a higher value when p = 0.5 and takes on the lowest value when p = 0 or 1.
At p = 0.5 the probability of an event is unpredictable and when p = 0 or 1 the probability is certain. Entropy shows the degree of predictability of an event.

Calculating Entropy
def entropy(p):
    if p == 0 or p == 1:
        return 0
    else:
        return -p * np.log2(p) - (1- p)*np.log2(1 - p)

def split_indices(X, index_feature):
    """
    X is the training data, and index_feature is the index of the
    feature we are splitting on.

    For every training example, determine whether it belongs to the
    left or right node based on the value of the selected feature.

    If the selected feature is present (1) in that example, the example goes to the left node.
    If the selected feature is absent (0) in that example, the example goes to the right node.

    For example:
        left_indices  = [1, 4, 5]
        right_indices = [0, 2, 3, 6, 7, 8]

    This means training examples 1, 4, and 5 belong to the left node,
    while examples 0, 2, 3, 6, 7, and 8 belong to the right node.
    """

    left_indices = []
    right_indices = []

    for i, x in enumerate(X):
        if x[index_feature] == 1:
            left_indices.append(i)
        else:
            right_indices.append(i)

    return left_indices, right_indices

Calculate the weighted entropy for each split

def weighted_entropy(X,y,left_indices,right_indices):
    """
    This function takes the splitted dataset, the indices we chose to split and returns the weighted entropy.
    w_left and w_right is the proportion of examples in each node
    p_left and p_right the proportion of cats in each split.
    """
    w_left = len(left_indices)/len(X)
    w_right = len(right_indices)/len(X)
    p_left = sum(y[left_indices])/len(left_indices)
    p_right = sum(y[right_indices])/len(right_indices)
    
    weighted_entropy = w_left * entropy(p_left) + w_right * entropy(p_right)
    return weighted_entropy

    Calculate Information gain
    def information_gain(X, y, left_indices, right_indices):
        """
        Here, X has the elements in the node and y is theirs respectives classes
        """
        p_node = sum(y)/len(y)
        h_node = entropy(p_node)
        w_entropy = weighted_entropy(X,y,left_indices,right_indices)
        return h_node - w_entropy

Now to calculate IG for each feature.

for i, feature_name in enumerate(['Ear Shape', 'Face Shape', 'Whiskers']):
    left_indices, right_indices = split_indices(X_train, i)
    i_gain = information_gain(X_train, y_train, left_indices, right_indices)
    print(f"Feature: {feature_name}, information gain if we split the root node using this feature: {i_gain:.2f}")
    
