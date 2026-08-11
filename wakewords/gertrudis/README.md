### Configuration

~~~
CONFIG = {
    'WAKE_WORD_NAME': 'gertrudis',         # output directory and model name
    'CLIP_DURATION_MS': 1500,              # 1500 for single word, 1800 for two words
    'PROBABILITY_CUTOFF': 0.85,            # start low (0.5) to test, raise to reduce false positives

    # TEST_VARIANTS: all candidates to listen in Cell 5. Pick the best in Cell 5b.
    'TEST_VARIANTS': ['gertrudis', 'gertru-dis'],
    'SAMPLES_PER_COMBO': 250,              # samples per variant+voice combo (total = variants x voices x this)

    # Check available languages/voices/qualities at https://rhasspy.github.io/piper-samples/
    'LANGUAGE': 'es_ES',                   # piper language code (es_ES, en_US, de_DE, fr_FR, ...)
    'VOICE_QUALITY': 'medium',             # low, medium, or high (not all qualities available for all languages)

    'NEGATIVE_CLASS_WEIGHT': 20,           # increase to reduce false positives (at cost of sensitivity)
    'TRAINING_STEPS': 10000,               # more steps = longer training, potentially better model
    'EVAL_STEP_INTERVAL': 2000,            # how often to evaluate (lower = more checkpoints, more RAM)

    # Evaluates false positive rate against long audio during training. Causes OOM on Colab free tier (T4 GPU).
    # Enable on paid Colab or CPU with enough RAM (needs ~4GB extra).
    'USE_DINNER_PARTY_EVAL': False,
}
~~~

### Output

~~~
INFO:absl:So far the best minimization quantity is 0.000 with best maximization quantity of 0.00000%; no faph cutoff is 0.00
INFO:absl:Step #4000: rate 0.001000, accuracy 99.95%, recall 99.71%, precision 99.68%, cross entropy 0.001472
2026-08-10 19:02:11.085127: W external/local_xla/xla/tsl/framework/cpu_allocator_impl.cc:84] Allocation of 32640000 exceeds 10% of free system memory.
INFO:absl:Step 4000 (nonstreaming): Validation: recall at no faph = 0.000 with cutoff 0.00, accuracy = 94.70%, recall = 94.70%, precision = 100.00%, ambient false positives = 0, estimated false positives per hour = 0.00000, loss = 0.32068, auc = 0.00000, average viable recall = 0.000000000
INFO:absl:So far the best minimization quantity is 0.000 with best maximization quantity of 0.00000%; no faph cutoff is 0.00
INFO:absl:Step #6000: rate 0.001000, accuracy 99.95%, recall 99.70%, precision 99.66%, cross entropy 0.001391
2026-08-10 19:13:51.415841: W external/local_xla/xla/tsl/framework/cpu_allocator_impl.cc:84] Allocation of 32640000 exceeds 10% of free system memory.
INFO:absl:Step 6000 (nonstreaming): Validation: recall at no faph = 0.000 with cutoff 0.00, accuracy = 96.40%, recall = 96.40%, precision = 100.00%, ambient false positives = 0, estimated false positives per hour = 0.00000, loss = 0.12947, auc = 0.00000, average viable recall = 0.000000000
INFO:absl:So far the best minimization quantity is 0.000 with best maximization quantity of 0.00000%; no faph cutoff is 0.00
INFO:absl:Step #8000: rate 0.001000, accuracy 99.97%, recall 99.75%, precision 99.81%, cross entropy 0.000993
2026-08-10 19:25:22.222171: W external/local_xla/xla/tsl/framework/cpu_allocator_impl.cc:84] Allocation of 32640000 exceeds 10% of free system memory.
INFO:absl:Step 8000 (nonstreaming): Validation: recall at no faph = 0.000 with cutoff 0.00, accuracy = 97.70%, recall = 97.70%, precision = 100.00%, ambient false positives = 0, estimated false positives per hour = 0.00000, loss = 0.14983, auc = 0.00000, average viable recall = 0.000000000
INFO:absl:So far the best minimization quantity is 0.000 with best maximization quantity of 0.00000%; no faph cutoff is 0.00
INFO:absl:Step #10000: rate 0.001000, accuracy 99.99%, recall 99.93%, precision 99.88%, cross entropy 0.000491
INFO:absl:Step 10000 (nonstreaming): Validation: recall at no faph = 0.000 with cutoff 0.00, accuracy = 97.00%, recall = 97.00%, precision = 100.00%, ambient false positives = 0, estimated false positives per hour = 0.00000, loss = 0.21894, auc = 0.00000, average viable recall = 0.000000000
INFO:absl:So far the best minimization quantity is 0.000 with best maximization quantity of 0.00000%; no faph cutoff is 0.00
INFO:absl:Sharding callback duration: 201 microseconds
~~~
