<template>
  <div class="demo">
    <h2>Horizontal Tabs</h2>
    <TabGroup orientation="horizontal">
      <TabItem>
        <template #header>Tab 1</template>
        <div class="tab-content">
          Content for Tab 1
        </div>
      </TabItem>
      <TabItem :active="true">
        <template #header>Tab 2</template>
        <div class="tab-content">
          Content for Tab 2
        </div>
      </TabItem>
      <TabItem>
        <template #header>Tab 3</template>
        <div class="tab-content">
          Content for Tab 3
        </div>
      </TabItem>
    </TabGroup>

    <h2 class="mt-8">Vertical Tabs</h2>
    <TabGroup orientation="vertical">
      <TabItem :active="true">
        <template #header>Tab 1</template>
        <div class="tab-content">
          Content for Tab 1
        </div>
      </TabItem>
      <TabItem>
        <template #header>Tab 2</template>
        <div class="tab-content">
          Content for Tab 2
        </div>
      </TabItem>
      <TabItem>
        <template #header>Tab 3</template>
        <div class="tab-content">
          Content for Tab 3
        </div>
      </TabItem>
    </TabGroup>
  </div>
</template>

<style>
.demo {
  max-width: 800px;
  margin: 2rem auto;
  padding: 1rem;
}

.mt-8 {
  margin-top: 2rem;
}

.tab-content {
  background-color: #f9fafb;
  padding: 1rem;
  border-radius: 0.5rem;
}
</style>