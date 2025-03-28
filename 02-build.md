<h2 class="cyan">Setup a CI Pipeline</h2>
<hr class="cyan">
<br><br>

## Let's create a pipeline

Select **Unified View** from the list \
   ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/module_unified.png)

> 1) Click on **Pipelines** in the left Nav \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/nav_pipelines.png)
> 1) Click `+Create Pipeline` \
>     ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_create.png)

> **Create new Pipeline**
> - Name: <pre>`Workshop Build and Deploy`</pre>
> - Store: `Inline`
> - Click **Start**

> [!NOTE]
> Inline vs. Remote - We're using inline for this lab, but you can also use a remote repository like GitHub. This is useful for teams that want to keep their *pipelines as code* bundled up snuggly with *application code*. Cozy!

> 1) Click `+Add Stage`
> 1) Choose **Build** stage type \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_stage_build.png)
> 1) Configure with the details below ↓

> **Build Stage**
> - Stage Name: <pre>`Build`</pre>
> - Clone Codebase: `Enabled`
> - Repository Name: `[[ Instruqt-Var key="HARNESS_REPO" hostname="sandbox" ]]`
> - Click **Set Up Stage**

> - On the **Infrastructure** tab \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_tab_infrastructure.png)
>    1) Select `Cloud`
>    1) Click **Continue >**

> [!NOTE]
> ***Harness Cloud is the BESTEST cloud*** <br>
> Something awesome happened right there. With zero configuration (well ok... ooooooone click!) you instantly configured an autoscaling build environment in the cloud that requires no management on your part and is dramatically less expensive than on-premise.

> - On the **Execution** tab \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_tab_execution.png)
> - Follow the instructions below to add ***three*** steps to our pipeline:
>    1) **Execute Unit Tests**
>    1) **Compile Application**
>    1) **Build and Push Artifact**

> 1) Add a step to execute unit tests
>    1) Select `Add Step`, then `Add Step` again
>    1) Select `Test Intelligence` from the Step Library \
>       ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/unscripted-workshop-2024/assets/images/unscripted_pipeline_build_test_intelligence.png)
>    1) Configure with the details below ↓

> **Test Intelligence**
> - Name: <pre>`Test Intelligence`</pre>
> - Command:
>  ```
>  cd ./python-tests
>  pytest
>  ```
> - Click **Apply Changes** in the top right

> [!NOTE]
> ***What is Test Intelligence?*** <br>
> Test Intelligence helps accelerate test cycles by up to 80%. By running only relevant tests, you can achieve faster builds, shorter feedback loops, and significant cost savings.

> 2) Add a step to compile our application
>    1) Select `Add Step`, then `Use template`
>    1) To standardize our build, a template has been precreated \
>     *Feel free to open up the template if you'd like to see what it's doing*
>    1) Select the `Compile Application` template
>    1) Click `Use template`
>    1) Configure with the details below ↓

> **Template**
> - Name: <pre>`Compile`</pre>
> - Click **Apply Changes** in the top right


> 3) Add a step to build and push our artifact
>    1) Select `Add Step`, then `Add Step` again
>    1) Select `Build and Push to GAR` from the Step Library \
>       ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_step_build_gar.png)
>    1) Configure with the details below ↓

> [!WARNING]
> Double check that you've selected \
> `Build and Push to GAR` \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_step_build_gar.png)
> And haven't accidentally selected \
> `Build and Push to GCR` \
>    ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_step_build_gcr.png)

> **Build and Push to GAR**
> - Name: <pre>`Push to Google Artifact Registry`</pre>
> - GCP Connector: `workshop-gar`
> - Host: <pre>`us-docker.pkg.dev`</pre>
> - Project Id: <pre>`seworkshop/seworkshop`</pre>
> - Image Name: <pre>`harness-workshop`</pre>
> - Tags:
>   - Click `+ Add`
>    <pre><code><+variable.username>-<+pipeline.sequenceId></code></pre>
> - **Optional Configuration  ⏷** \
>    *(Required for this Lab)*
>   - Dockerfile: <pre>`/harness/frontend-app/harness-webapp/Dockerfile`</pre>
>   - Context: <pre>`/harness/frontend-app/harness-webapp`</pre>
> - Click **Apply Changes** in the top right

### Execute your new Pipeline
> Click **Save** in the top right to save your new pipeline. \
>   ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_save.png)

> Now click **Run** to execute the pipeline \
>   ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/assets/images/pipeline_run.png)
> Then click **Run Pipeline** \
>   ![](https://raw.githubusercontent.com/harness-community/field-workshops/main/se-workshop-devsecops/assets/images/pipeline_run_pipeline.png)

> [!NOTE]
> You might have noticed an option to pick the branch before running the pipeline. We're using `main` for simplicity, but it's a great example of how this complete build pipeline could easily be reused for other branches (or repositories or services).

![](https://raw.githubusercontent.com/harness-community/field-workshops/main/unscripted-workshop-2024/assets/images/unscripted_lab2_execution.png)

===============

Click the **Next** button to continue.
