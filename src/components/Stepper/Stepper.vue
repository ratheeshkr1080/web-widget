<template>
  <div>Stepper</div>

  <!-- <div className={classes.root}>
      <Stepper activeStep={activeStep}>
        {steps.map((label, index) => {
          const stepProps = {};
          const labelProps = {};
          if (isStepOptional(index)) {
            labelProps.optional = <Typography variant="caption">Optional</Typography>;
          }
          if (isStepSkipped(index)) {
            stepProps.completed = false;
          }
          return (
            <Step key={label} {...stepProps}>
              <StepLabel {...labelProps}>{label}</StepLabel>
            </Step>
          );
        })}
      </Stepper>
      <div>
        {activeStep === steps.length ? (
          <div>
            <Typography className={classes.instructions}>
              All steps completed - you&apos;re finished
            </Typography>
            <Button onClick={handleReset} className={classes.button}>
              Reset
            </Button>
          </div>
        ) : (
          <div>
            <Typography className={classes.instructions}>{getStepContent(activeStep)}</Typography>
            <div>
              <Button disabled={activeStep === 0} onClick={handleBack} className={classes.button}>
                Back
              </Button>
              {isStepOptional(activeStep) && (
                <Button
                  variant="contained"
                  color="primary"
                  onClick={handleSkip}
                  className={classes.button}
                >
                  Skip
                </Button>
              )}

              <Button
                variant="contained"
                color="primary"
                onClick={handleNext}
                className={classes.button}
              >
                {activeStep === steps.length - 1 ? 'Finish' : 'Next'}
              </Button>
            </div>
          </div>
        )}
      </div>
    </div> -->
</template>
<script>
function getSteps() {
  return ["Select campaign settings", "Create an ad group", "Create an ad"];
}

// function getStepContent(step) {
//   switch (step) {
//     case 0:
//       return "Select campaign settings...";
//     case 1:
//       return "What is an ad group anyways?";
//     case 2:
//       return "This is the bit I really care about!";
//     default:
//       return "Unknown step";
//   }
// }

//   const steps = getSteps();

//   const isStepOptional = (step) => {
//     return step === 1;
//   };

//   const isStepSkipped = (step) => {
//     return skipped.has(step);
//   };

//   const handleNext = () => {
//     let newSkipped = skipped;
//     if (isStepSkipped(activeStep)) {
//       newSkipped = new Set(newSkipped.values());
//       newSkipped.delete(activeStep);
//     }

//     setActiveStep((prevActiveStep) => prevActiveStep + 1);
//     setSkipped(newSkipped);
//   };

//   const handleBack = () => {
//     setActiveStep((prevActiveStep) => prevActiveStep - 1);
//   };

//   const handleSkip = () => {
//     if (!isStepOptional(activeStep)) {
//       // You probably want to guard against something like this,
//       // it should never occur unless someone's actively trying to break something.
//       throw new Error("You can't skip a step that isn't optional.");
//     }

//     setActiveStep((prevActiveStep) => prevActiveStep + 1);
//     setSkipped((prevSkipped) => {
//       const newSkipped = new Set(prevSkipped.values());
//       newSkipped.add(activeStep);
//       return newSkipped;
//     });
//   };

//   const handleReset = () => {
//     setActiveStep(0);
//   };

export default {
  name: "Stepper",
  props: {},
  data() {
    return {
      activeStep: "",
      skipped: new Set(),
      steps: getSteps(),
    };
  },

  methods: {
    isStepOptional(step) {
      return step === 1;
    },
    isStepSkipped(step) {
      return this.skipped.has(step);
    },

    handleNext() {
      let newSkipped = this.skipped;
      if (this.isStepSkipped(this.activeStep)) {
        newSkipped = new Set(newSkipped.values());
        newSkipped.delete(this.activeStep);
      }

      // setActiveStep((prevActiveStep) => prevActiveStep + 1);
      this.activeStep = (prevActiveStep) => prevActiveStep + 1;
      // setSkipped(newSkipped);
      this.skipped = newSkipped;
    },

    handleBack() {
      // setActiveStep((prevActiveStep) => prevActiveStep - 1);
      this.activeStep = (prevActiveStep) => prevActiveStep - 1;
    },

    handleSkip() {
      if (!this.isStepOptional(this.activeStep)) {
        // You probably want to guard against something like this,
        // it should never occur unless someone's actively trying to break something.
        throw new Error("You can't skip a step that isn't optional.");
      }

      // setActiveStep((prevActiveStep) => prevActiveStep + 1);
      this.activeStep = (prevActiveStep) => prevActiveStep + 1;
      // setSkipped((prevSkipped) => {
      //   const newSkipped = new Set(prevSkipped.values());
      //   newSkipped.add(activeStep);
      //   return newSkipped;
      // });
      this.skipped = (prevSkipped) => {
        const newSkipped = new Set(prevSkipped.values());
        newSkipped.add(this.activeStep);
        return newSkipped;
      };
    },

    handleReset() {
      this.setActiveStep(0);
    },
  },
};
</script>

<style scoped>
</style>