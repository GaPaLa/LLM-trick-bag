
# the first tokens always have highest loss because no context - theory: this forces lots of the parameters in the LM to be taken up to lower their loss, but we are actualy not interested in this - we are always providing the model a question and asking it to asnwer it. We should pretrain it to just output the answer
# EXCEPT - multiple people have found that finetuning LLMs on Q&A gets lower loss than just A. What papers look into this seriously? I do notice myself predicting what people will say next and even interrupting them. 
# at the same time, training an LLM on both question and answer is like training an RL model to provide both the environment and the actions. - actually this is not true - self supervised learning on video probably helps them, which is the same thing. hmmm.. whats th difference?
# well, we definitely cant get a good prediction from 0 context, so just drop the first few highest loss tokens so the LLM loss can focus parameters on its own output, rather than modelling the user.

# in text-image diffusion [] and audio models [] we see taht retreival helps long tail cases. we asee langauge is long tail case because Adam is needed over SGD.






# ==== stuff to test

# heirarchical RNN + transfo?
# reduces slow leraning induced by dealing with a tokenizer, also
# only uses large transformer layers where high level intellgience is needed (e.g. see "variable grouped query attention" paper) - probably dont need to reach far back for token-level stuff, only complicated semantic stuff








# ====================== OPTIMIZATIONS
# padding stuffing - padding takes up compute without doing anything. replace apdded tokens with 

# flash attention 2

# variable grouped query attention





# ====================== faster learning
# RETRO - create a knowledge graph - how to know what knowledge is useful? Seed tasks -> find important documents via embedding similarity -> extract key extracts -> pre-embed [IF YOU WANT TO BUILD THE KNOWLDGE GRAPH AS YOU GO, YOU NEED TO APPLY A LOT OF NOISE TO IT, otherwise it will get used to seeing the exact same examples -> knowledge graph node dropout, standard dropout on embeddings, add gaussian noise to embeddings]

# memorizing transformer

# implement early exit (CALM)

# use single-wide FFW for parameter efficiency.

# potentially? branch-train-merge - training 3 smaller models then merging gets higher accuracy faster than training one big one. Maybe do this iteratively throughout training?

# data cleaning - skill-it skill graph builder?; beating neural scling laws with data pruning; 

# Symbol Tuning

# use low perplexity tokens (from METAmath paper, also I suspect teh reason for TinyStories and textbooks are all you need)




# ========================== continual learning = ICL + retrieval
train for better in context learning performance
https://arxiv.org/pdf/2307.00119.pdf

# instead o starting prompt with "you are a helpful assistant" start with with "hi, i am helpful AI assistant"

# RL: do ReST + plus "lengauge model is better reward model when given 2 prompts to compare in context"

# from BERT cramming:
# triangle leraning rate? rly?
# 






# =========== ROBUSTNESS

# gradient starvation
# top down and lateral model connections

# weight decay -> rank decay? -> better proxy for sparsity [@TODO research]





# ========== LOSS

next token prediction loss is not long term enough, we want the model to say something because it has thought of something good to say in response to the context, not come up with something good in reponse to the context because it said something.

i.e. when a charcter level LM predict token e, its not becuase it thought of some answer that starts with e, its because the largest number of possible answers start with e, so its the most likely token.

we want a loss that incientivises 100% token confidence because it is trying to say something specific

i.e. its a certain type of mode collapse when instead f modelling a single likely output, its just risk minimization to output the average of allppossible outputs. slightly different though because that IS the loss - risk minimization. GANs are kind of a way out of this but they also suffer mode collapse - diffusion models arent like this though! they do not at all come up with something generic just because its a good middle ground betwewen answers - they create very very specific and strong outputs! maybe we should train LLMs with latent diffusion loss - train target abstract idea to say.

Do latent diffusion with language! let each latent output possibly output many or few words. pass them to a smaller model. so, we split text into chunks intelligently and get it to predict the next chunk.




# ========== inference time performance improvements

# contrastive decoding https://huggingface.co/papers/2309.09117
