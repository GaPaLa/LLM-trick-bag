# padding stuffing - padding takes up compute without doing anything. replace apdded tokens with 

# the first tokens always have highest loss because no context - theory: this forces lots of the parameters in the LM to be taken up to lower their loss, but we are actualy not interested in this - we are always providing the model a question and asking it to asnwer it. We should pretrain it to just output the answer
# EXCEPT - multiple people have found that finetuning LLMs on Q&A gets lower loss than just A. What papers look into this seriously? I do notice myself predicting what people will say next and even interrupting them. 
# at the same time, training an LLM on both question and answer is like training an RL model to provide both the environment and the actions. - actually this is not true - self supervised learning on video probably helps them, which is the same thing. hmmm.. whats th difference?
# well, we definitely cant get a good prediction from 0 context, so just drop the first few highest loss tokens so the LLM loss can focus parameters on its own output, rather than modelling the user.

# in text-image diffusion [] and audio models [] we see taht retreival helps long tail cases. we asee langauge is long tail case because Adam is needed over SGD.

# contrastive decoding https://huggingface.co/papers/2309.09117

# use single-wide FFW for parameter efficiency.

# implement early exit (CALM)

# implement grouped query attention

# implement 

# heirarchical RNN + transfo?

# data cleaning - skill-it skill tree builder?

# memorising transformer

# RETRO - create a knowledge graph - how to know what knowledge is useful? Seed tasks -> find important documents via embedding similarity -> extract key extracts -> pre-embed [IF YOU WANT TO BUILD THE KNOWLDGE GRAPH AS YOU GO, YOU NEED TO APPLY A LOT OF NOISE TO IT, otherwise it will get used to seeing the exact same examples -> knowledge graph node dropout, standard dropout on embeddings, add gaussian noise to embeddings]

# instead o starting prompt with "you are a helpful assistant" start with with "hi, i am helpful AI assistant"

# RL: do ReST + plus "lengauge model is better reward model when given 2 prompts to compare in context"

# from BERT cramming:
# triangle leraning rate? rly?
# 

# RBOUSTNESS

# gradient starvation
# top down and lateral model connections